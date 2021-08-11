<template>
  <br>
  <nav class="navbar navbar-expand navbar-light bg-light" style="margin-left:50px;">
      <div class="nav navbar-nav">
          <router-link to="/crear" class="nav-link">Crear</router-link>
          <router-link to="/listar" class="nav-link">Empleados</router-link> 
      </div>
  </nav>  
  <router-view/>
</template>

