# LojaTesteConhecimento
Esse projeto é voltado para o teste de conhecimentos técnicos em Desenvolvimento de Sistemas.

Corrigir o validador "apenasNumeros" para aceitar pontos e virgulas e criar o sistema voltado para encerrar compra.

    package loja.aprimorada;
    import java.util.Scanner;
    import static loja.aprimorada.MetodosDeFuncao.carrinho;
    import static loja.aprimorada.MetodosDeFuncao.produto;
    import static loja.aprimorada.MetodosDeFuncao.encerrarCompras;
    import static loja.aprimorada.Utilidades.ajusteVetorCarrinho;
    import static loja.aprimorada.Utilidades.ajusteVetorProdutos;
    import static loja.aprimorada.Utilidades.limpa;
    //@author Pedro Gusmao
    //@author Tainá Carvalho
    public class LojaAprimorada {                   
        public static void main(String[] args) {
            Scanner leia = new Scanner(System.in);
            boolean repetir = false;
            int opcao;
            String validador;
            ajusteVetorProdutos();
            ajusteVetorCarrinho();
            while(repetir == false){
                System.out.println("==================__M E N U__==================");
                System.out.println("Escolha um opção:\n1) Adicionar produtos\t3) Encerrar Compras\n2) Carrinho\t\t4) Encerrar Programa");
                validador = leia.nextLine();
                if(Validadores.apenasNumeros(validador)){
                    opcao = Integer.parseInt(validador);
                    limpa();            
                    switch(opcao){
                        case 1:
                            produto();
                        break;
                        case 2: 
                            carrinho();
                        break;
                        case 3:
                            encerrarCompras();
                        break;
                        case 4:
                            double soma = 0;      
                            for (int i = 0; i < 20; i++) {
                                if(BancoDeDados.carrinhoPreco[i] != -1){
                                    soma += BancoDeDados.carrinhoPreco[i];
                                }
                            }
                            System.out.println("\n\nEm produtos adicionados, você tem um total de: R$ "+soma);
                            System.out.println("Você optou pelo fim!!");
                            System.exit(0);
                        break;
                        default:
                            repetir = false;
                            System.out.println("Escolha uma opção valida!!");
                    }
                }else{
                    limpa();
                    System.out.println("\nDigite apenas numeros!\n");
                }
            }
        }  
    }   // '-'
