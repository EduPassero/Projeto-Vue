<template>
	<div>
		<titulo :texto="professorid != undefined ? 'Professor: ' + professor.nome : 'Todos os Alunos'" />
		<div v-if="professorid != undefined">
			<input type="text" placeholder="Nome do Aluno" v-model="nome" @keyup.enter="addAluno()" />
			<button class="btn btnInput" @click="addAluno()">Adicionar</button>
		</div>
		<table>
			<thead>
				<th>Mat.</th>
				<th>Nome</th>
				<th>Opções</th>
			</thead>
			<tbody v-if="alunos.length">
				<tr v-for="(aluno, index) in alunos" :key="index">
					<td>{{aluno.id}}</td>
					<router-link :to="`/alunoDetalhe/${aluno.id}`" tag="td" style="cursor:pointer">{{aluno.nome}}</router-link>
					<td>
						<button class="btn btn_danger" @click="removeAluno(aluno)">Remover</button>
					</td>
				</tr>
			</tbody>
			<tfoot v-else>Ora porra!</tfoot>
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
			titulo: "Alunos",
			professorid: this.$route.params.prof_id,
			professor: {},
			nome: "",
			alunos: []
		};
	},

	created() {
		if (this.professorid) {
			this.carregaProfessores();
			this.$http
				.get("http://localhost:3000/alunos?professor.id=" + this.professorid)
				.then(res => res.json())
				.then(alunos => (this.alunos = alunos));
		} else {
			this.$http
				.get("http://localhost:3000/alunos?")
				.then(res => res.json())
				.then(alunos => (this.alunos = alunos));
		}
	},

	props: {},

	methods: {
		addAluno() {
			let _aluno = {
				nome: this.nome,
				sobrenome: "",
				professor: {
					id: this.professor.id,
					nome: this.professor.nome
				}
			};

			this.$http
				.post("http://localhost:3000/alunos", _aluno)
				.then(res => res.json())
				.then(alunoRetornado => {
					this.alunos.push(alunoRetornado);
					this.nome = "";
				});
		},

		removeAluno(aluno) {
			this.$http.delete(`http://localhost:3000/alunos/${aluno.id}`).then(() => {
				let indice = this.alunos.indexOf(aluno);
				this.alunos.splice(indice, 1);
			});
		},

		carregaProfessores() {
			this.$http
				.get("http://localhost:3000/professores/" + this.professorid)
				.then(res => res.json())
				.then(professorRetornado => {
					this.professor = professorRetornado;
				});
		}
	}
};
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
input {
	width: calc(100% - 195px);
	border: 0;
	padding: 20px;
	font-size: 1.3em;
	color: #687f7f;
}

.btnInput {
	width: 153px;
	border: 0px;
	padding: 20px;
	font-size: 1.3em;
	background-color: #1c7e7e;
}

.btnInput:hover {
	padding: 20px;
	margin: 0px;
	border: 0px;
}
</style>
