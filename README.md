Identificação das violações dos princípios

Violação do ISP (Interface Segregation Principle)

No código apresentado existe uma interface chamada Funcionario que obriga todas as classes a implementarem vários métodos:
	•	trabalhar()
	•	registrarPonto()
	•	receberSalario()
	•	gerenciarEquipe()
	•	escreverCodigo()

O problema é que nem todos os funcionários precisam executar todas essas funções.

Por exemplo:
	•	O gerente não precisa escrever código.
	•	O desenvolvedor não precisa gerenciar equipe.
	•	O estagiário não recebe salário, mas sim uma bolsa.

Isso mostra que a interface está grande demais e força as classes a implementarem métodos que não utilizam.

Impacto no sistema

Isso faz com que algumas classes precisem lançar erros quando certos métodos são chamados. Isso deixa o sistema mais difícil de manter e pode causar problemas no funcionamento do programa.

⸻

Violação do LSP (Liskov Substitution Principle)

O princípio de substituição de Liskov diz que uma classe filha deve poder substituir a classe base sem causar problemas no sistema.

No código apresentado, algumas classes lançam erros em métodos que não fazem sentido para elas, como por exemplo:
	•	Desenvolvedor lançando erro ao tentar gerenciar equipe.
	•	Estagiário lançando erro ao tentar receber salário.

Isso significa que o comportamento esperado da interface não é respeitado por todas as classes.

Impacto no sistema

Isso pode causar falhas no programa caso o sistema tente executar esses métodos esperando um comportamento válido.

⸻

Violação do DIP (Dependency Inversion Principle)

O sistema depende diretamente de uma interface muito grande e com várias responsabilidades.

O ideal seria dividir essa interface em várias interfaces menores, onde cada classe implementaria apenas o que realmente precisa.

Isso tornaria o sistema mais flexível e fácil de modificar no futuro.

2. Refatoração do código

Para resolver os problemas apresentados, podemos dividir a interface grande em interfaces menores.

Novas interfaces

interface Trabalhador {
 trabalhar(): void;
}

interface Programador {
 escreverCodigo(): void;
}

interface Assalariado {
 receberSalario(): void;
}

interface RegistradorPonto {
 registrarPonto(): void;
}

interface Gerenciavel {
 gerenciarEquipe(): void;
}

Classe Gerente

class Gerente implements Trabalhador, RegistradorPonto, Assalariado, Gerenciavel {

 trabalhar(): void {
  console.log("Gerente trabalhando");
 }

 registrarPonto(): void {
  console.log("Ponto registrado");
 }

 receberSalario(): void {
  console.log("Salário recebido");
 }

 gerenciarEquipe(): void {
  console.log("Gerenciando equipe");
 }

}

Classe Desenvolvedor

class Desenvolvedor implements Trabalhador, RegistradorPonto, Assalariado, Programador {

 trabalhar(): void {
  console.log("Desenvolvedor trabalhando");
 }

 registrarPonto(): void {
  console.log("Ponto registrado");
 }

 receberSalario(): void {
  console.log("Salário recebido");
 }

 escreverCodigo(): void {
  console.log("Escrevendo código");
 }

}

Classe Estagiário

class Estagiario implements Trabalhador, RegistradorPonto, Programador {

 trabalhar(): void {
  console.log("Estagiário trabalhando");
 }

 registrarPonto(): void {
  console.log("Ponto registrado");
 }

 escreverCodigo(): void {
  console.log("Estagiário escrevendo código");
 }

}

3. Nova classe Freelancer

class Freelancer implements Trabalhador, Programador {

 trabalhar(): void {
  console.log("Freelancer trabalhando");
 }

 escreverCodigo(): void {
  console.log("Freelancer escrevendo código");
 }

}
