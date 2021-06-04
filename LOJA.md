# LojaTesteConhecimento
Esse projeto é voltado para o teste de conhecimentos técnicos em Desenvolvimento de Sistemas.

package loja.aprimorada;
import java.util.Scanner;
public class LojaAprimorada {
    public static String[] produtos = new String[20];
    public static String[] carrinho = new String[20];
    public static double[] carrinhoPreco = new double [20];
    public static double[] precosProdutos = new double[20];
    public static void limpa(){
        for(int i = 0; i < 200; i++){   
            System.out.println("\r\n");
        }
    }
    public static void espera(){
        Scanner leia = new Scanner(System.in);
        String aguarde;
        System.out.println("\n\n================================================================");
        System.out.println("Pressione ENTER para continuar!!");
        aguarde = leia.nextLine();
    }
    public static void ajusteVetorProdutos(){ //    
        for(int i = 0; i < 20; i++){
            produtos[i] = "vazio";
            precosProdutos[i] = -1;
        }
    }
    public static void ajusteVetorCarrinho(){ //    
        for(int i = 0; i < 20; i++){
            carrinho[i] = "vazio";
            carrinhoPreco[i] = -1;
        }
    }
    public static void addNomeProduto(){
        Scanner leia = new Scanner(System.in);
        int slot = 0, itens = exibirProdutos();
        double validacao = 0;
        if(itens > 0){
            slot = itens;
        }
        while(slot < 20){
            validacao = 0;
            System.out.printf("\nDigite o nome do produto Nº %s: ",slot+1);
            produtos[slot] = leia.nextLine();  
            if("".equals(produtos[slot])){
                    produtos[slot] = "vazio";
                    produtos[slot] = leia.nextLine();
            }
            if("0".equals(produtos[slot])){
                produtos[slot] = "vazio";
                slot = 20;
            }else{
                while(validacao == 0){
                    System.out.printf("Digite o preço do produto N° %s: ",slot+1,"\n"); //a pessoa coloca o preço e tals
                    precosProdutos[slot] = leia.nextDouble();
                    if(precosProdutos[slot] == 0){
                        validacao = 0;
                        System.out.println("Você deve adicionar um preço!!\n");
                    }else{
                        validacao = 1;
                    }
                }
            }
            slot++;
        }
    }
    public static void addProdutoCarrinho(){
        Scanner leia = new Scanner(System.in);
        int indice, slot = 0, itens = exibirCarrinho();
        if(itens > 0){
            slot = itens;
        }
        while(slot < 20){
            exibirProdutos();
            System.out.printf("\nEscolha o Indice do produto nº %s que deseja: ",slot+1);
            indice = leia.nextInt(); 
            if(indice == 0){
                carrinho[slot] = "vazio";
                slot = 20;    
            }else{
                carrinho[slot] = produtos[indice-1];
                carrinhoPreco[slot] = precosProdutos[indice-1];
                if("".equals(carrinho[slot])){
                carrinho[slot] = "vazio";
                slot -= 1;
                }
            }
            limpa();
            realocar(2);
            slot++;
        }
    }
    public static int exibirProdutos(){
        System.out.println("Lista de Produtos!!");
        int itens = 0;
        for(int i = 0; i < 20; i++){            
            if("vazio".equals(produtos[i])){    
               //nada
            }else{
                if(i < 9){    
                    System.out.print("0"+(i+1)+" "+produtos[i]);
                    itens += 1;            
                    System.out.println("\t\t R$ "+precosProdutos[i]);
                }else{
                    System.out.print((i+1)+" "+produtos[i]);
                    itens += 1;
                    System.out.println("\t\t R$ "+precosProdutos[i]);
                }
            }
        }
        return itens;
    }
    public static int exibirCarrinho(){
        System.out.println("Lista do Carrinho!!");
        int itens = 0;
        for(int i = 0; i < 20; i++){            
            if("vazio".equals(carrinho[i])){    
               //nada
            }else{
                if(i < 9){    
                    System.out.print("0"+(i+1)+" "+carrinho[i]);
                    itens += 1;            
                    System.out.println("\t\t R$ "+carrinhoPreco[i]);
                }else{
                    System.out.print((i+1)+" "+carrinho[i]);
                    itens += 1;
                    System.out.println("\t\t R$ "+carrinhoPreco[i]);
                }
            }
        }
        return itens;
    }
    public static void realocar(int escolha){
        Double[] auxiliarPreco = new Double[20];
        String[] auxiliar = new String[20];
        for(int i = 0; i < 20; i++){
            auxiliar[i] = "vazio";
        }
        int indiceAux = 0;
        switch(escolha){
            case 1:
                System.arraycopy(produtos, 0, auxiliar, 0, 20);
                ajusteVetorProdutos();
                for(int slot = 0; slot < 20; slot++){
                    if("vazio".equals(auxiliar[slot])){
                       //nada
                    }else{                      
                       produtos[indiceAux] = auxiliar[slot]; 
                       indiceAux++;
                    }
                }
                break;
            case 2: 
                System.arraycopy(carrinho, 0, auxiliar, 0, 20);
                ajusteVetorCarrinho();
                for(int slot = 0; slot < 20; slot++){
                    if("vazio".equals(auxiliar[slot])){
                       //nada
                    }else{                      
                       carrinho[indiceAux] = auxiliar[slot]; 
                       indiceAux++;
                    }
                }
                break;
        }
    }
    public static void removerItem(int indice, int aferir){
        switch(aferir){    
            case 1:
                produtos[indice-1] = "vazio";
                precosProdutos[indice-1] = 0;
                realocar(1);
                break;
            case 2:
                carrinho[indice-1] = "vazio";
                carrinhoPreco[indice-1] = 0;
                realocar(2);
                break;
        }
    }
    public static void addProduto(){
        Scanner leia = new Scanner(System.in);
        int escolha, itens;
        boolean repetir = false;
        while(repetir == false){       
                System.out.println("==================__M E N U__P R O D U T O S__==================");
                System.out.println("Escolha um opção:\n1) Adicionar\t3) Visualizar\n2) Remover\t4) Inicio");
                escolha = leia.nextInt();
                limpa();                   
            switch (escolha) {
                case 1:
                    System.out.println("Software versão BETA, suporta apenas 20 itens!!");
                    System.out.println("Digite 0 para voltar para o Menu!!");
                    addNomeProduto();
                    exibirTotal(1);
                    limpa();
                    break;
                case 2:                                    
                    boolean repetirSub = false;
                    while(repetirSub == false){
                        int indice = 0;
                        itens = exibirProdutos();
                        System.out.println("\nEscolha o Indice do item que deseja remover.");
                        System.out.printf("Há %s itens na lista.\n",itens);
                        System.out.println("\n================================================================\n");
                        System.out.println("Digite 0 para voltar!!");
                        if(itens > 0){   
                            indice = leia.nextInt();
                        }else{
                                repetirSub = true;
                        }
                        if(indice == 0){
                            repetirSub = true;
                        }else{
                            removerItem(indice, 1);                     
                        }
                        limpa();
                    }
                    limpa();
                    break;
                case 3:                
                    System.out.println("Lista de Produtos!!");
                    itens = exibirProdutos();
                    if(itens == 0){    
                        System.out.println("\n================================================================");
                        System.out.println("L I S T A  V A Z I A !!");    
                        System.out.println("\n================================================================");
                        System.out.println("L I S T A  V A Z I A !!");
                    }else{
                        if(itens == 1){
                            System.out.printf("\nNa lista tem %s produto.",itens);
                            exibirTotal(1);
                        }else{
                            System.out.printf("\nNa lista tem %s produtos.",itens);
                            exibirTotal(1);
                        }  
                    }
                    espera();
                    limpa();
                    break;               
                case 4:
                    System.out.println("Você optou voltar para o inicio!!");
                    repetir = true;
                    break;                
                default:
                    System.out.println("Escolha uma opção válida!");
                    break; 
            }
        }
    }
    public static void Carrinho(){
        Scanner leia = new Scanner(System.in);
        boolean repetir = false;
        int escolha, itens;
        while(repetir == false){
            System.out.println("==================__M E N U__C A R R I N H O__==================");
            System.out.println("Escolha um opção:\n1) Adicionar\t3) Visualizar\n2) Remover\t4) Inicio");
            escolha = leia.nextInt();
            limpa();
            switch(escolha){
                case 1:
                    System.out.println("Software versão BETA, suporta apenas 20 itens!!");
                    System.out.println("Digite 0 para voltar para o Menu!!");
                    addProdutoCarrinho();
                    limpa();
                    break;
                case 2:
                    boolean repetirSub = false;
                    while(repetirSub == false){
                        int indice = 0;
                        itens = exibirProdutos();
                        System.out.println("Escolha o Indice do item que deseja remover.");
                        System.out.printf("Há %s itens na lista.\n",itens);
                        System.out.println("\n================================================================\n");
                        System.out.println("Digite 0 para voltar!!");
                        if(itens > 0){   
                            indice = leia.nextInt();
                        }else{
                                repetirSub = true;
                        }
                        if(indice == 0){
                            repetirSub = true;
                        }else{
                            removerItem(indice, 2);                     
                        }
                        limpa();
                    }
                    limpa();
                    break;
                case 3:
                    itens = exibirCarrinho();
                    if(itens == 0){    
                        System.out.println("\n================================================================");
                        System.out.println("L I S T A  V A Z I A !!");    
                        System.out.println("\n================================================================");
                        System.out.print("L I S T A  V A Z I A !!");
                    }else{
                        if(itens == 1){
                            System.out.printf("\nNa lista tem %s produto.",itens);
                            exibirTotal(2);
                        }else{
                            System.out.printf("\nNa lista tem %s produtos.",itens);
                            exibirTotal(2);
                        }
                    }
                    espera();
                    limpa();
                    break;
                case 4:
                    System.out.println("Você optou voltar para o inicio!!");
                    repetir = true;
                    break;
                default:
                    System.out.println("Escolha uma opção válida!");
                    break;
            }
        }
    }    
    public static void exibirTotal(int opc){
        double soma = 0;
        int length = precosProdutos.length;
        switch(opc){
            case 1:
                for (int i = 0; i < 20; i++) {
                    int slot = 0;
                    if(slot == -1){
                        soma = 0;
                    }else if(slot != -1 || slot != 0){
                        soma = precosProdutos[slot] + precosProdutos[slot+1];
                    }
                    slot++;
                }
                System.out.print("\n\nEm produtos adicionados, você tem um total de: R$ "+soma);
                espera();
                limpa();
                break;
            case 2:
                for (int i = 0; i < 20; i++) {
                    int slot = 0;
                    if(slot == -1){
                        soma = 0;
                    }else if(slot != -1 || slot != 0){
                        soma = carrinhoPreco[slot] + carrinhoPreco[slot+1];
                    }
                    slot++;
                }
                System.out.print("\n\nOs produtos adicionados no seu carrinho de um total de: R$ "+soma);
                limpa();
                break;
        }
    }
    public static void main(String[] args) {
        Scanner leia = new Scanner(System.in);
        boolean repetir = false;
        int opcao;
        ajusteVetorProdutos();
        ajusteVetorCarrinho();
        while(repetir == false){
            System.out.println("==================__M E N U__==================");
            System.out.println("Escolha um opção:\n1) Adicionar produtos\t3) Salario\n2) Carrinho\t\t4) Encerrar");
            opcao = leia.nextInt();
            limpa();            
            switch(opcao){
                case 1:
                    addProduto();
                break;
                case 2: 
                    Carrinho();
                break;
                case 3:
                break;
                case 4:
                    double soma = 0;
                    int length = precosProdutos.length;       //aqui deixei aparecer o preço do produto pq o preço do carrinho n tá funcionando! Aí foi só pra testar mesmo, por enquanto
                    for (int i = 0; i < 20; i++) {
                        int slot = 0;
                        if(slot == -1){
                            soma = 0;
                        }else if(slot != -1 || slot != 0){
                            soma = precosProdutos[slot] + precosProdutos[slot+1];
                        }
                        slot++;
                    }
                    System.out.println("\n\nEm produtos adicionados, você tem um total de: R$ "+soma);
                    System.out.println("Você optou pelo fim!!");
                    System.exit(0);
                break;
                default:
                    repetir = false;
                    System.out.println("Escolha uma opção valida!!");
            }
        }
    }  
}   // visualizar carrinho bugou pra mim '-'
