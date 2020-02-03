<template>
	<div id="app">
		<Nav></Nav>
		<div class="marginPrincipal">
			<router-view :key="$route.fullPath"></router-view>
		</div>
	</div>
</template>

<script>
import Nav from "./components/_nav/Nav";

export default {
	name: "app",
	components: {
		Nav
	}
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Montserrat:400,700");

body {
	background-color: rgb(247, 247, 247);
	font-family: "Montserrat", sans-serif;
	display: grid;
	justify-items: center;
}
body,
html {
	margin: 0;
	height: 100%;
}

.marginPrincipal {
	width: 50%;
	margin: auto;
}

#app {
	width: 100%;
}
.btn_danger {
	font-size: 0.8em !important;
	background-color: rgb(204, 28, 28);
}
.btn {
	padding: 10px, 20px;
	cursor: pointer;
	border: 1px solid rgb(97, 97, 97);
	color: white;
	font-size: 1.2em;
	font-weight: bold;
	border-radius: 5px;
	border-bottom: 3px solid rgb(138, 84, 84);
}
.btn:hover {
	text-shadow: 1px 1px 1px rgb(158, 156, 156);
	margin-top: 3px;
	border-bottom: 1px solid rgb(138, 84, 84);
}

table {
	margin: 0px;
	padding: 0px;
	list-style-type: none;
	width: 100%;
}
table tr td {
	padding: 20px;
	font-size: 1.3em;
	background-color: #e0edf4;
	margin-bottom: 2px;
	color: #3e5252;
}
table thead th {
	background-color: rgb(184, 208, 216) !important;
	font-size: 1.2em;
	padding: 10px 0px;
	text-align: center !important;
}
.colPequeno {
	width: 5%;
}
</style>
