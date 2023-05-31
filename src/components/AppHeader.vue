<script>

    export default {
        name: "AppHeader",
        data() {
            return {
                menuItems: [
                    {
                        label: 'Home',
                        routeName: 'home'
                    },
                    {
                        label: 'Projects',
                        routeName: 'projects'
                    },
                    {
                        label: 'Contattami',
                        routeName: 'contact'
                    },
                    {
                        label: 'About',
                        routeName: 'about'
                    }
                ]
            }
        }
    }

</script>

<template>

<nav class="navbar mb-5 bg-dark" data-bs-theme="dark">
  <div class="container-fluid">
    <a class="navbar-brand text-white">Navbar</a>
    <ul class="navbar-nav me-auto mb-2 mb-lg-0">
      <li class="nav-item" v-for="item in menuItems"> 
        <router-link :to="{name: item.routeName}" class="nav-link">{{item.label}}</router-link>
      </li>
    </ul>
    <form class="d-flex" role="search">
      <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
      <button class="btn btn-outline-primary" type="submit">Search</button>
    </form>
  </div>
</nav>
  
</template>

<style>


</style>