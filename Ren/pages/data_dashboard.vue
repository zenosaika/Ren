<template lang="html">
  <div class="container-fluid">
    <div class="row">
      <div class="col-3">
        <div class="card">
          <div class="row">
            <div class="col-6">
              <p style="color: #ccc">
                <span style="font-size: 12px">Number of</span><br />Customers
              </p>
            </div>
            <div class="col-6 stat">
              <p style="color: #008ffb">
                {{ number_of_user.customer }}
              </p>
            </div>
          </div>
        </div>
      </div>

      <div class="col-3">
        <div class="card">
          <div class="row">
            <div class="col-6">
              <p style="color: #ccc">
                <span style="font-size: 12px">Number of</span><br />Supporters
              </p>
            </div>
            <div class="col-6 stat">
              <p style="color: #57ffc4">
                {{ number_of_user.supporter }}
              </p>
            </div>
          </div>
        </div>
      </div>

      <div class="col-3">
        <div class="card">
          <div class="row">
            <div class="col-6">
              <p style="color: #ccc">
                <span style="font-size: 12px">Number of</span><br />Videos
              </p>
            </div>
            <div class="col-6 stat">
              <p style="color: #ff8598">{{ number_of_video }}</p>
            </div>
          </div>
        </div>
      </div>

      <div class="col-3">
        <div class="card">
          <div class="row">
            <div class="col-6">
              <p style="color: #ccc">
                <span style="font-size: 12px">Download</span><br />Data
              </p>
            </div>
            <div class="col-6 stat">
              <p style="font-size: 20px; color: #777">JSON | CSV</p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="row">
      <div class="col-4">
        <div class="box shadow" style="margin-top: 0px; margin-bottom: 0px">
          <client-only>
            <ApexCharts
              :options="circle_params.options"
              :series="circle_params.series"
              :height="265"
              :width="400"
            />
          </client-only>
        </div>
      </div>
      <div class="col-8">
        <div class="box shadow" style="margin-top: 0px; margin-bottom: 0px">
          <client-only>
            <ApexCharts
              :options="line_params.options"
              :series="line_params.series"
              :height="250"
              :width="800"
            />
          </client-only>
        </div>
      </div>
    </div>

    <div class="row">
      <div class="col-8">
        <div class="box shadow" style="height: 80%">
          <client-only>
            <ApexCharts
              :options="bar_params.options"
              :series="bar_params.series"
              :height="250"
              :width="820"
            />
          </client-only>
        </div>
      </div>
      <div class="col-4">
        <div class="box shadow">
          <client-only>
            <ApexCharts
              :options="donut_params.options"
              :series="donut_params.series"
              :height="230"
              :width="400"
            />
          </client-only>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import donut_chart from '../static/graph_options/donut_chart.json'
import line_chart from '../static/graph_options/line_chart.json'
import bar_chart from '../static/graph_options/bar_chart.json'
import circle_chart from '../static/graph_options/circle_chart.json'

export default {
  async asyncData({ $axios }) {
    const number_of_user = await $axios
      .$get('http://localhost:4000/api/v1/get/user')
      .then((res) => {
        const customer = res.data.filter((x) => x.role === 3).length
        const supporter = res.data.filter((x) => x.role === 2).length
        return { customer, supporter }
      })
    const bar_params = await $axios
      .$get('http://localhost:4000/api/v1/get/message')
      .then((res) => {
        const customer_messages = res.data.filter(
          (x) => x.sender_user_id === x.receiver_user_id
        )
        const today = new Date() // get current date and time
        const day_offset = 60 * 60 * 24 * 1000
        const message_count = {}

        for (let n = 20; n >= 0; n--) {
          const n_day_offset = day_offset * n
          const n_day_ago = new Date(today.getTime() - n_day_offset)
          const date = `${n_day_ago.getDate()}/${
            n_day_ago.getMonth() + 1
          }/${n_day_ago.getFullYear()}`
          message_count[date] = 0
        }

        for (let i = 0; i < customer_messages.length; i++) {
          const timestamp = parseInt(customer_messages[i].timestamp)
          const datetime = new Date(timestamp)
          const date = `${datetime.getDate()}/${
            datetime.getMonth() + 1
          }/${datetime.getFullYear()}`
          if (date in message_count) {
            message_count[date] += 1
          }
        }
        const month = [
          'Jan',
          'Feb',
          'Mar',
          'Apr',
          'May',
          'Jun',
          'Jul',
          'Aug',
          'Sep',
          'Oct',
          'Nov',
          'Dec',
        ]

        const labels = []
        let series = []
        for (const date in message_count) {
          const tmp = date.split('/')
          const day = tmp[0]
          labels.push(`${day} ${month[parseInt(tmp[1]) - 1]}`)
          series.push(message_count[date])
        }
        const options = bar_chart.options
        options.labels = labels
        series = [{ name: 'Customer Messages', data: series }]
        return { options, series }
      })
    const number_of_video = await $axios
      .$get('http://localhost:4000/api/v1/get/video')
      .then((res) => res.data.length)
    const package_table = await $axios
      .$get('http://localhost:4000/api/v1/get/package')
      .then((res) => {
        const package_table = {}
        for (let i = 0; i < res.data.length; i++) {
          const package_id = res.data[i].package_id
          if (!(package_id in package_table)) {
            package_table[package_id] = res.data[i]
          }
        }
        return package_table
      })
    const donut_params = await $axios
      .$get('http://localhost:4000/api/v1/get/user')
      .then((res) => {
        const labels = []
        let series = {}
        for (const key in package_table) {
          const package_id = package_table[key].package_id
          const package_name = package_table[key].package_name
          labels.push(package_name)
          series[package_id] = 0
        }
        series[-1] = 0
        labels.push('No Subscription')
        const user = res.data
        for (let i = 0; i < user.length; i++) {
          if (user[i].role === 3) {
            const package_id = user[i].package_id
            if (!package_id) {
              series[-1] += 1
            } else {
              series[user[i].package_id] += 1
            }
          }
        }
        const tmp_series = []
        for (const key in series) {
          tmp_series.push(series[key])
        }
        series = tmp_series
        const options = donut_chart.options
        options.labels = labels
        return { options, series }
      })
    const line_params = await $axios
      .$get('http://localhost:4000/api/v1/get/bill')
      .then((res) => {
        let series = {}
        for (const key in package_table) {
          series[key] = {
            name: package_table[key].package_name,
            data: new Array(12).fill(0),
          }
        }
        const bills = res.data
        const today = new Date()
        for (let i = 0; i < bills.length; i++) {
          const package_id = `${bills[i].package_id}`
          const start_timestamp = parseInt(bills[i].start_timestamp)
          if (
            Math.abs(today.getTime() - start_timestamp) / 60 / 60 / 24 / 1000 <
            365
          ) {
            const month = new Date(start_timestamp).getMonth()
            if (month !== today.getMonth()) series[package_id].data[month] += 1
          }
        }
        const tmp_series = []
        for (const key in series) {
          const name = series[key].name
          const data = series[key].data
          tmp_series.push({ name, data })
        }
        for (let i = 0; i < tmp_series.length; i++) {
          tmp_series[i].data = tmp_series[i].data
            .slice(today.getMonth() + 1)
            .concat(tmp_series[i].data.slice(0, today.getMonth() + 1))
        }
        series = tmp_series
        const options = line_chart.options
        const month = [
          'Jan',
          'Feb',
          'Mar',
          'Apr',
          'May',
          'Jun',
          'Jul',
          'Aug',
          'Sep',
          'Oct',
          'Nov',
          'Dec',
        ]
        const labels = month
          .slice(today.getMonth() + 1)
          .concat(month.slice(0, today.getMonth() + 1))
        options.labels = labels
        return { options, series }
      })

    const circle_params = await $axios
      .$get('http://localhost:4000/api/v1/get/user')
      .then((res) => {
        const labels = []
        let series = {}
        for (const key in package_table) {
          const package_id = package_table[key].package_id
          const package_name = package_table[key].package_name
          labels.push(package_name)
          series[package_id] = { n_all: 0, n_continue_renewal: 0 }
        }
        const user = res.data
        for (let i = 0; i < user.length; i++) {
          if (user[i].role === 3) {
            const package_id = user[i].package_id
            if (package_id) {
              series[package_id].n_all += 1
              if (user[i].is_auto_renewal === 1) {
                series[package_id].n_continue_renewal += 1
              }
            }
          }
        }
        const tmp_series = []
        for (const key in series) {
          const percent = parseInt(
            (series[key].n_continue_renewal / series[key].n_all) * 100
          )
          tmp_series.push(percent)
        }
        series = tmp_series
        const options = circle_chart.options
        options.labels = labels
        return { options, series }
      })

    return {
      number_of_user,
      bar_params,
      number_of_video,
      line_params,
      package_table,
      donut_params,
      circle_params,
    }
  },
}
</script>

<style lang="css" scoped>
.box {
  backdrop-filter: blur(16px) saturate(180%);
  -webkit-backdrop-filter: blur(16px) saturate(180%);
  background-color: rgba(17, 25, 40, 0.5);
  border-radius: 12px;
  border: 1px solid rgba(255, 255, 255, 0.125);
  padding: 25px;
  margin: 20px;
}

.shadow {
  box-shadow: 0px 1px 15px 1px rgba(69, 65, 78, 0.08);
}

.card {
  backdrop-filter: blur(16px) saturate(180%);
  -webkit-backdrop-filter: blur(16px) saturate(180%);
  background-color: rgba(17, 25, 40, 0.5);
  border-radius: 12px;
  border: 1px solid rgba(255, 255, 255, 0.125);
  padding: 10px 20px 0px 20px;
  margin: 20px;
}

.stat {
  font-family: 'Roboto Condensed', sans-serif;
  font-size: 28px;
  font-weight: 600;
  display: flex;
  align-items: center;
  position: relative;
  top: 4px;
}
</style>
