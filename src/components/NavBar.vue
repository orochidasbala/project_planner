<template>
    <nav class="main-nav">
        <router-link to="/">Projects</router-link> |  
        <router-link :to="{ name: 'addProject' }">Add Project</router-link>
    </nav>
</template>
<script>
export default {};
</script>
<style>
.main-nav {
	margin: 40px auto;
    text-align: center;
}
.main-nav a {
	display: inline-block;
	margin: 0 5px;
    text-transform: uppercase;
    color: rgb(192, 100, 228);
    text-decoration: none;
	font-weight: 800;
	font-size: 18px;
}
a.router-link-active { 
	border-bottom: 2px solid rgba(124, 124, 124, 0.37);
	padding: 2px 1px;
}
</style>