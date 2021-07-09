# LojaTesteConhecimento
Esse projeto é voltado para o teste de conhecimentos técnicos em Desenvolvimento de Sistemas.
    
    package loja.aprimorada;
    import java.util.Scanner;
    import static loja.aprimorada.MetodosDeFuncao.realocar;

    public class Utilidades {
        public static void espera(){
            Scanner leia = new Scanner(System.in);
            String aguarde;
            System.out.println("\n\n================================================================");
            System.out.println("Pressione ENTER para continuar!!");
            aguarde = leia.nextLine();
        }
        public static void ajusteVetorProdutos(){ //    
            for(int i = 0; i < 20; i++){
                BancoDeDados.produtos[i] = "vazio";
                BancoDeDados.produtoPreco[i] = -1;
            }
        }
        public static void ajusteVetorCarrinho(){ //    
            for(int i = 0; i < 20; i++){
                BancoDeDados.carrinho[i] = "vazio";
                BancoDeDados.carrinhoPreco[i] = -1;
            }
        }
        public static void limpa(){
            for(int i = 0; i < 200; i++){   
                System.out.println("\r\n");
            }
        }
        public static int totalProdutos(){      
            int itens = 0;
            for(int i = 0; i < 20; i++){            
                if("vazio".equals(BancoDeDados.produtos[i])){    
                   //nada
                }else{                                 
                    itens += 1;                                    
                }
            }
            return itens;
        }
        public static void removerItem(int indice, int aferir){
            switch(aferir){    
                case 1:
                    BancoDeDados.produtos[indice-1] = "vazio";
                    BancoDeDados.produtoPreco[indice-1] = -1;
                    realocar(1);
                    break;
                case 2:
                    BancoDeDados.carrinho[indice-1] = "vazio";
                    BancoDeDados.carrinhoPreco[indice-1] = -1;
                    realocar(2);
                    break;
            }
        }
    }
