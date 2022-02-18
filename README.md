# ACADEMIA-CAPGEMINI
DESAFIO DE PROGRAMAÇÃO - ACADEMIA CAPGEMINI


public class Main {
	// questão 01
	public static void escada(int n) {
		int i, j, aux = n;
		for (i = 0; i < n; i++) {
			while (aux > 0) {
				System.out.print(" ");
				aux--;
			}
			aux = (n - 1) - i;

			for (j = aux; j < n; j++) {
				System.out.print("*");
			}
			System.out.println("");
		}
	}

	// questão 02
	public static int senha(String senha) {
		int cont = 0, i;
		int v[];
		v = new int[4];
		char[] str = senha.toCharArray();

		if (senha.length() >= 6) {
			for (i = 0; i < senha.length(); i++) {
				if (str[i] >= 48 && str[i] <= 57) {
					v[0]++;
				} else if (str[i] >= 65 && str[i] <= 90) {
					v[1]++;
				} else if (str[i] >= 97 && str[i] <= 122) {
					v[2]++;
				} else if (str[i] >= 33 && str[i] <= 47 || str[i] >= 58 && str[i] <= 64 || str[i] >= 91 && str[i] <= 96
						|| str[i] >= 123 && str[i] <= 126) {
					v[3]++;
				}
			}
			for (i = 0; i < v.length; i++) {
				if (v[i] == 0)
					cont++;
			}
		} else {
			cont = 6 - senha.length();
		}

		return cont;
	}

	// questão 03
	public static boolean verificaAnagrama(String s1, String s2) {
		char[] cs1 = s1.toCharArray();
		char[] cs2 = s2.toCharArray();
		int pos2, pos1 = 0;
		boolean encontrado, ok = true;

		while (pos1 < s1.length() && ok) {
			pos2 = 0;
			encontrado = false;
			while (pos2 < cs2.length && !encontrado) {
				if (cs1[pos1] == cs2[pos2]) {
					encontrado = true;
				} else {
					pos2++;
				}
			}
			if (encontrado)
				cs2[pos2] = Character.MIN_VALUE;
			else
				ok = false;
			pos1++;
		}

		return ok;
	}

	public static int verificaSubs(String s1, String og) {
		char[] strc = og.toCharArray();
		String s2 = "";
		int n = strc.length, len, i, j, k, cont = 0;
		for (len = 1; len <= n; len++) {
			for (i = 0; i <= n - len; i++) {
				j = i + len - 1;
				for (k = i; k <= j; k++) {
					s2 = s2 + strc[k];
				}
				if (s1.length() == s2.length()) {
					if (verificaAnagrama(s1, s2))
						cont++;
				}
				s2 = "";
			}
		}
		return cont;
	}

	public static int anagrama(String str) {
		char[] strc = str.toCharArray();
		String s1 = "";
		int n = strc.length, len, i, j, k, cont = 0;
		for (len = 1; len <= n; len++) {
			for (i = 0; i <= n - len; i++) {
				j = i + len - 1;
				for (k = i; k <= j; k++) {
					s1 = s1 + strc[k];
				}
				cont = cont + verificaSubs(s1, str);
				s1 = "";
			}
		}
		return cont;
	}

	public static void main(String[] args) {
		System.out.println("Exercicio 1:");
		escada(6);
		System.out.println("\nExercicio 2:");
		System.out.println("" + senha("Aaaa!a"));
		System.out.println("\nExercicio 3:");
		System.out.println(anagrama("ovo"));
	}

}
