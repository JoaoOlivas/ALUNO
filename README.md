CLASSE ALUNO

public class Aluno {
    private String matricula;
    private String nome;
    private String email;

    public Aluno(String matricula, String nome, String email) {
        this.matricula = matricula;
        this.nome = nome;
        this.email = email;
    }

    // Getters e Setters
    public String getMatricula() {
        return matricula;
    }

    public void setMatricula(String matricula) {
        this.matricula = matricula;
    }

    public String getNome() {
        return nome;
    }

    public void setNome(String nome) {
        this.nome = nome;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    @Override
    public String toString() {
        return "Aluno{" +
                "matricula='" + matricula + '\'' +
                ", nome='" + nome + '\'' +
                ", email='" + email + '\'' +
                '}';
    }
}

CLASSE TURMA

import java.util.ArrayList;
import java.util.List;

public class Turma {
    private String nomeDisciplina;
    private int numeroTurma;
    private List<Aluno> alunos;
    private int tamanhoTurma;

    public Turma(String nomeDisciplina, int numeroTurma, int tamanhoTurma) {
        this.nomeDisciplina = nomeDisciplina;
        this.numeroTurma = numeroTurma;
        this.tamanhoTurma = tamanhoTurma;
        this.alunos = new ArrayList<>();
    }

    // Adicionar aluno
    public boolean adicionarAluno(Aluno aluno) {
        if (alunos.size() >= tamanhoTurma) {
            System.out.println("Turma cheia. Não é possível adicionar mais alunos.");
            return false;
        }
        for (Aluno a : alunos) {
            if (a.getMatricula().equals(aluno.getMatricula())) {
                System.out.println("Aluno com matrícula " + aluno.getMatricula() + " já está na turma.");
                return false;
            }
        }
        alunos.add(aluno);
        return true;
    }

    @Override
    public String toString() {
        StringBuilder sb = new StringBuilder();
        sb.append("Turma{" +
                "nomeDisciplina='" + nomeDisciplina + '\'' +
                ", numeroTurma=" + numeroTurma +
                ", alunos=[\n");
        for (Aluno aluno : alunos) {
            sb.append(aluno.toString()).append("\n");
        }
        sb.append("]}");
        return sb.toString();
    }
}

CLASSE PRINCIPAL

import java.util.Scanner;

public class Principal {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Digite o nome da disciplina: ");
        String nomeDisciplina = scanner.nextLine();

        System.out.print("Digite o número da turma: ");
        int numeroTurma = scanner.nextInt();

        System.out.print("Digite o tamanho da turma: ");
        int tamanhoTurma = scanner.nextInt();
        scanner.nextLine(); // Consumir a nova linha

        Turma turma = new Turma(nomeDisciplina, numeroTurma, tamanhoTurma);

        // Cadastro de 2 alunos manualmente
        for (int i = 0; i < 2; i++) {
            System.out.print("Digite a matrícula do aluno " + (i + 1) + ": ");
            String matricula = scanner.nextLine();

            System.out.print("Digite o nome do aluno " + (i + 1) + ": ");
            String nome = scanner.nextLine();

            System.out.print("Digite o e-mail do aluno " + (i + 1) + ": ");
            String email = scanner.nextLine();

            Aluno aluno = new Aluno(matricula, nome, email);
            turma.adicionarAluno(aluno);
        }

        // Exibir a turma
        System.out.println(turma);

        scanner.close();
    }
}
