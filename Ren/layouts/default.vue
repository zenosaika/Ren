<template>
  <div>
    <div>
      <nav class="navbar navbar-expand-lg navbar-custom px-3">
        <a class="navbar-brand" href="/">PYTHONFLIX</a>
        <div class="collapse navbar-collapse">
          <ul class="navbar-nav me-auto">
            <li class="nav-item">
              <a class="nav-link" href="/">Home</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#">Profile</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="/support_chat">Support Chat</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="/data_dashboard">Data Dashboard</a>
            </li>
          </ul>
        </div>
        <div class="collapse navbar-collapse">
          <ul class="navbar-nav ms-auto">
            <li class="nav-item">
              <a class="nav-link" style="color: rgb(156, 232, 43)" href="#"
                >Login</a
              >
            </li>
            <li class="nav-item">
              <a class="nav-link" style="color: rgb(156, 232, 43)" href="#"
                >Register</a
              >
            </li>
          </ul>
        </div>
      </nav>
    </div>
    <Nuxt />
  </div>
</template>

<style>
body {
  background: #0f0c29; /* fallback for old browsers */
  background: -webkit-linear-gradient(
    to right,
    #24243e,
    #302b63,
    #0f0c29
  ); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(
    to right,
    #24243e,
    #302b63,
    #0f0c29
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
}

.navbar-custom {
  background-color: #1d2638;
}

.navbar-custom .navbar-brand {
  font-family: 'Bebas Neue', cursive;
  font-size: 2rem;
  color: #e50914;
  padding: 0px;
}

.navbar-custom .nav-link {
  color: #ccc;
}
</style>
