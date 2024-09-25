package Velha129;
import java.util.Scanner;
public class JogoDaVelha {
   public static void main(String[] args) {
       Scanner in = new Scanner(System.in);
		System.out.println("Bem vindo ao Jodo Da Velha!");
		System.out.println("\n");
		// Nome dos jogadores
		System.out.println("Jogador 1, Qual seu nome?");
		String p1 = in.nextLine();
		System.out.println("Jogador 2, Qual seu nome?");
		String p2 = in.nextLine();
		char[][] tabuleiro = new char[4][4];
		// Preencher o tabuleiro
		for (int i = 1; i < 4; i++) {
			for (int j = 1; j < 4; j++) {
				tabuleiro[i][j] = '-';
			}
		}
		// De quem é a vez de jogar
		boolean isJogador1 = true;
		//Verificar fim de jogo
		boolean fimDeJogo = false;	
		while(!fimDeJogo) {
		// Desenhar tabuleiro
		desenharTab(tabuleiro);
		// Símbolo usado para jogo
		char simbolo = ' ';
		if (isJogador1) {
			simbolo = 'x';
		} else {
			simbolo = 'o';
		}
		// print a vez do jogador
		if (isJogador1) {
			System.out.println("Vez de " + p1 + " (x) ");
		} else {
			System.out.println("Vez de " + p2 + " (o) ");
		}
		int linha = 1;
		int coluna = 1;
		while (true) {
			// Obter linha e coluna do jogador
			System.out.print("Escolha uma linha (1,2 ou 3):");
			linha = in.nextInt();
			System.out.print("Escolha uma coluna (1,2 ou 3):");
			coluna = in.nextInt();
			// Testar se linha e coluna são válidas
			if (linha < 1 || coluna < 1 || linha > 3 || coluna > 3) {
				System.out.println(" Inválido! ");
			} else if (tabuleiro[linha][coluna] != '-') {
				System.out.println(" Já preenchido! ");
			} else {
				// válidos
				break;
			}
		}
		// Definir posições no tabuleiro com respectivos símbolos
		tabuleiro[linha][coluna] = simbolo;
		// Verificar qual jogador ganhou
		if (vencedor(tabuleiro) == 'x') {
			// Jogador 1 ganhador
			System.out.println(p1 + " Venceu!");
			fimDeJogo = true;
		} else if (vencedor(tabuleiro) == 'o') {
			// Jogador 2 ganhador
			System.out.println(p2 + " Venceu!");
			fimDeJogo = true;	
		} else {
			if (velha(tabuleiro)) {
				// empate
				System.out.println("Velha!");
				fimDeJogo = true;
			} else {
				// Continuar jogo
            isJogador1 = !isJogador1;
			}
		}
	 }
	//Print tabuleiro final
	desenharTab(tabuleiro);
	}
	// Imprimir tabuleiro
	public static void desenharTab(char[][] tabuleiro) {
		for (int i = 1; i < 4; i++) {
			for (int j = 1; j < 4; j++) {
				System.out.print("   " +  tabuleiro[i] [j]);
			}
			System.out.println("\n");
		}
	}
	public static char vencedor(char[][] tabuleiro) {
		// linha
		for (int i = 1; i < 4; i++) {
			if (tabuleiro[i][1] == tabuleiro[i][2] && tabuleiro[i][2] == tabuleiro[i][3] && tabuleiro[i][1] != '-') {
				return tabuleiro[i][1];
			}
		}
		// coluna
		for (int j = 1; j < 4; j++) {
			if (tabuleiro[1][j] == tabuleiro[2][j] && tabuleiro[2][j] == tabuleiro[3][j] && tabuleiro[1][j] != '-') {
				return tabuleiro[1][j];
			}
		}
		// Diagonais
		if (tabuleiro[1][1] == tabuleiro[2][2] && tabuleiro[2][2] == tabuleiro[3][3] && tabuleiro[1][1] != '-') {
			return tabuleiro[1][1];
		}
		if (tabuleiro[3][1] == tabuleiro[2][2] && tabuleiro[2][2] == tabuleiro[1][3] && tabuleiro[3][1] != '-') {
			return tabuleiro[3][1];
		}
		// Ninguém ganhou
		return '-';
	}
	// Verificar se o tabuleiro está cheio/empate
	public static boolean velha(char[][] tabuleiro) {
		for (int i = 1; i < 4; i++) {
			for (int j = 1; j < 4; j++) {
				if (tabuleiro[i][j] == '-') {
					return false;
				}
			}
		}
		return true;
	}
}

