<template>
	<div>
		<titulo :texto="`Aluno: ${aluno.nome}`" :btnVoltar="!editor">
			<button v-show="editor" class="btn btnEditar" @click="editar()">Editar</button>
		</titulo>

		<table>
			<tbody>
				<tr>
					<td class="colPequeno">Matrícula:</td>
					<td>
						<label>{{aluno.id}}</label>
					</td>
				</tr>
				<tr>
					<td class="colPequeno">Nome:</td>
					<td>
						<label v-if="editor">{{aluno.nome}}</label>
						<input v-else v-model="aluno.nome" />
					</td>
				</tr>
				<tr>
					<td class="colPequeno">Sobrenome:</td>
					<td>
						<label v-if="editor">{{aluno.sobrenome}}</label>
						<input v-else v-model="aluno.sobrenome" />
					</td>
				</tr>
				<tr>
					<td class="colPequeno">Data de Nascimento:</td>
					<td>
						<label v-if="editor">{{aluno.dataNasc}}</label>
						<input v-else v-model="aluno.dataNasc" />
					</td>
				</tr>
				<tr>
					<td class="colPequeno">Professor:</td>
					<td>
						<label v-if="editor">{{aluno.professor.nome}}</label>
						<select v-else v-model="aluno.professor">
							<option
								v-for="(professor, index) in professores"
								:key="index"
								v-bind:value="professor"
							>{{professor.nome}}</option>
						</select>
					</td>
				</tr>
			</tbody>
		</table>

		<div style="margin-top: 10px;">
			<div v-if="!editor">
				<button class="btn btnSalvar" @click="salvar(aluno)">Salvar</button>
				<button class="btn btnCancelar" @click="cancelar()">Cancelar</button>
			</div>
		</div>
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
			editor: true,
			professores: [],
			aluno: {},
			idAluno: this.$route.params.id
		};
	},

	created() {
		this.$http
			.get("http://localhost:3000/alunos/" + this.idAluno)
			.then(res => res.json())
			.then(alunoRetornado => (this.aluno = alunoRetornado));

		this.$http
			.get("http://localhost:3000/professores")
			.then(res => res.json())
			.then(professor => (this.professores = professor));
	},

	methods: {
		editar() {
			this.editor = !this.editor;
		},

		salvar(_aluno) {
			let _alunoEditar = {
				id: _aluno.id,
				nome: _aluno.nome,
				sobrenome: _aluno.sobrenome,
				dataNasc: _aluno.dataNasc,
				professor: _aluno.professor
			};

			this.$http.put(
				`http://localhost:3000/alunos/${_alunoEditar.id}`,
				_alunoEditar
			);

			this.editor = !this.editor;
		},

		cancelar() {
			this.editor = !this.editor;
		}
	}
};
</script>

<style scoped>
.colPequeno {
	width: 20%;
	text-align: right;
	background-color: rgb(125, 217, 220);
	font-weight: bold;
}

.btnEditar {
	float: right;
	background-color: rgb(17, 140, 197);
}

.btnSalvar {
	float: right;
	background-color: rgb(11, 201, 175);
}

.btnCancelar {
	float: left;
	background-color: rgb(197, 53, 17);
}

input,
select {
	margin: 0px;
	padding: 5px 10px;
	font-size: 0.9em;
	border-radius: 5px;
	font-family: montserrat, sans-serif;
	border: 1px solid silver;
	width: 95%;
	background-color: rgb(245, 245, 245);
}
</style>