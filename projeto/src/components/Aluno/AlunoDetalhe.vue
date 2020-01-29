<template>
	<div>
		<titulo :texto="`Aluno: ${aluno.nome}`" />
		<table>
			<tbody>
				<tr>
					<td class="colPequeno">Matrícula:</td>
					<td>
						<label>{{aluno.id}}</label>
					</td>
				</tr>
				<tr>
					<td>Nome:</td>
					<td>
						<label>{{aluno.nome}}</label>
						<input v-model="aluno.nome" />
					</td>
				</tr>
				<tr>
					<td>Sobrenome:</td>
					<td>
						<label>{{aluno.sobrenome}}</label>
						<input v-model="aluno.sobrenome" />
					</td>
				</tr>
				<tr>
					<td>Data de Nascimento:</td>
					<td>
						<label>{{aluno.dataNasc}}</label>
						<input v-model="aluno.dataNasc" />
					</td>
				</tr>
				<tr>
					<td>Professor:</td>
					<td>
						<label>{{aluno.professor.nome}}</label>
						<!-- <input v-model="aluno.professor" /> -->
					</td>
				</tr>
			</tbody>
		</table>
	</div>
</template>

<script>
import Titulo from "../_share/Titulo";
export default {
	components: {
		Titulo
	},

	data() {
		return {
			aluno: {},
			idAluno: this.$route.params.id
		};
	},

	created() {
		this.$http
			.get("http://localhost:3000/alunos/" + this.idAluno)
			.then(res => res.json())
			.then(alunoRetornado => (this.aluno = alunoRetornado));
	},

	methods: {}
};
</script>

<style lang="css" scoped>
</style>