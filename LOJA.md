# LojaTesteConhecimento
Esse projeto é voltado para o teste de conhecimentos técnicos em Desenvolvimento de Sistemas.

    package loja.aprimorada;

    import java.util.Scanner;
    import static loja.aprimorada.Utilidades.ajusteVetorCarrinho;
    import static loja.aprimorada.Utilidades.ajusteVetorProdutos;
    import static loja.aprimorada.Utilidades.espera;
    import static loja.aprimorada.Utilidades.limpa;
    import static loja.aprimorada.Utilidades.totalProdutos;
    import static loja.aprimorada.Utilidades.removerItem;
    import static loja.aprimorada.Validadores.apenas_s_ou_n;

    public class MetodosDeFuncao {
        public static void addNomeProduto(){
            Scanner leia = new Scanner(System.in);
            int slot = 0, itens = exibirProdutos();
            double validacaoValor = 0;
            String validador;
            if(itens > 0){
                slot = itens;
            }
            while(slot < 20){
                validacaoValor = 0;
                while(validacaoValor == 0){
                    System.out.printf("\nDigite o nome do produto Nº %s: ",slot+1);
                    BancoDeDados.produtos[slot] = leia.nextLine();  
                    if("".equals(BancoDeDados.produtos[slot])){
                            System.out.printf("\nDigite o nome do produto Nº %s: ",slot+1);
                            BancoDeDados.produtos[slot] = "vazio";
                            BancoDeDados.produtos[slot] = leia.nextLine();
                    }
                    if("".equals(BancoDeDados.produtos[slot])){
                        validacaoValor = 0;
                        BancoDeDados.produtos[slot] = "vazio";
                        System.out.println("\nDigite um nome!!");
                    }else{
                        validacaoValor = 1;
                    }
                }
                validacaoValor = 0;
                if("0".equals(BancoDeDados.produtos[slot])){
                    BancoDeDados.produtos[slot] = "vazio";
                    slot = 20;
                }else{
                    while(validacaoValor == 0){
                        System.out.printf("Digite o preço do produto N° %s: ",slot+1,"\n"); //a pessoa coloca o preço e tals
                        validador = leia.nextLine();
                        if(Validadores.apenasNumeros(validador)){
                            BancoDeDados.produtoPreco[slot] =  Double.parseDouble(validador);                                       
                            if(BancoDeDados.produtoPreco[slot] == 0){
                                validacaoValor = 0;
                                System.out.println("\nVocê deve adicionar um preço!!\n");
                            }else{
                                validacaoValor = 1;
                            }
                        }else{
                            System.out.println("\nDigite apenas numeros!!\n");
                        }
                    }
                }
                slot++;
            }
        }
        public static void addProdutoCarrinho(){
            Scanner leia = new Scanner(System.in);
            int indice, slot = 0, itens = exibirCarrinho(), quantidade = totalProdutos();
            if(itens > 0){
                slot = itens;    
            }
            boolean carrinhoVazio = "vazio".equals(BancoDeDados.produtos[0]);
            if(!carrinhoVazio){    
                while(slot < 20){
                    String validador;
                    exibirProdutos();
                    System.out.printf("\nEscolha o Indice do produto nº %s que deseja: ",slot+1);
                    validador = leia.nextLine();
                    if(Validadores.apenasNumeros(validador)){
                        indice = Integer.parseInt(validador);
                        if(indice <= quantidade){   
                            if(indice == 0){
                                BancoDeDados.carrinho[slot] = "vazio";
                                slot = 20;
                            }else{
                                BancoDeDados.carrinho[slot] = BancoDeDados.produtos[indice-1];
                                BancoDeDados.carrinhoPreco[slot] = BancoDeDados.produtoPreco[indice-1];
                                if("".equals(BancoDeDados.carrinho[slot])){
                                    BancoDeDados.carrinho[slot] = "vazio";
                                    slot -= 1;
                                }
                            }
                        }else{
                            System.out.println("\nEscolha uma opção valida!");
                            slot--;
                            espera();
                        }
                    }else{
                        System.out.println("\nDigite apenas numeros!\n");
                        espera();
                    }
                    limpa();
                    realocar(2);
                    slot++;
                    System.out.println("Digite 0 para voltar!\n");
                }
            }else{
                limpa();
                System.out.println("Não há produtos adicionados a lista de produtos!");
                espera();
            }
        }
        public static int exibirProdutos(){
            System.out.println("Lista de Produtos!!");
            int itens = 0;
            for(int i = 0; i < 20; i++){            
                if("vazio".equals(BancoDeDados.produtos[i])){    
                   //nada
                }else{
                    if(i < 9){    
                        System.out.print("0"+(i+1)+" "+BancoDeDados.produtos[i]);
                        itens += 1;            
                        System.out.println("\t\t R$ "+BancoDeDados.produtoPreco[i]);
                    }else{
                        System.out.print((i+1)+" "+BancoDeDados.produtos[i]);
                        itens += 1;
                        System.out.println("\t\t R$ "+BancoDeDados.produtoPreco[i]);
                    }
                }
            }
            return itens;
        }
        public static int exibirCarrinho(){
            int itens = 0;
            for(int i = 0; i < 20; i++){            
                if("vazio".equals(BancoDeDados.carrinho[i])){    
                   //nada
                }else{
                    if(i < 9){    
                        System.out.print("0"+(i+1)+" "+BancoDeDados.carrinho[i]);
                        itens += 1;            
                        System.out.println("\t\t R$ "+BancoDeDados.carrinhoPreco[i]);
                    }else{
                        System.out.print((i+1)+" "+BancoDeDados.carrinho[i]);
                        itens += 1;
                        System.out.println("\t\t R$ "+BancoDeDados.carrinhoPreco[i]);
                    }
                }
            }
            return itens;
        }
        public static void exibirTotal(int opc){
            double soma = 0;
            switch(opc){
                case 1:
                    for (int i = 0; i < 20; i++) {
                        if(BancoDeDados.produtoPreco[i] != -1){
                            soma += BancoDeDados.produtoPreco[i];
                        }
                    }
                    System.out.print("\n\nEm produtos adicionados, você tem um total de: R$ "+soma);
                    break;
                case 2:
                    for (int i = 0; i < 20; i++) {
                        int slot = 0;
                        if(BancoDeDados.carrinhoPreco[i] != -1){
                            soma += BancoDeDados.carrinhoPreco[i];
                        }
                    }
                    System.out.print("\n\nOs produtos adicionados no seu carrinho, deu um total de: R$ "+soma);
                    break;
            }
        }
        public static void realocar(int escolha){
            Double[] auxiliarPreco = new Double[20];
            String[] auxiliar = new String[20];
            for(int i = 0; i < 20; i++){
                auxiliar[i] = "vazio";
                auxiliarPreco[i] = 0.0;
            }
            int indiceAux = 0;
            switch(escolha){
                case 1:
                    for(int indice = 0; indice < 20; indice++){
                        auxiliar[indice] = BancoDeDados.produtos[indice];
                        auxiliarPreco[indice] = BancoDeDados.produtoPreco[indice];
                    }
                    ajusteVetorProdutos();
                    for(int slot = 0; slot < 20; slot++){
                        if("vazio".equals(auxiliar[slot])){
                           //nada
                        }else{                      
                           BancoDeDados.produtos[indiceAux] = auxiliar[slot];
                           BancoDeDados.produtoPreco[indiceAux] = auxiliarPreco[slot];
                           indiceAux++;
                        }
                    }
                    break;
                case 2: 
                    for(int indice = 0; indice < 20; indice++){
                        auxiliar[indice] = BancoDeDados.carrinho[indice];
                        auxiliarPreco[indice] = BancoDeDados.carrinhoPreco[indice];
                    }
                    ajusteVetorCarrinho();
                    for(int slot = 0; slot < 20; slot++){
                        if("vazio".equals(auxiliar[slot])){
                           //nada
                        }else{                      
                           BancoDeDados.carrinho[indiceAux] = auxiliar[slot];
                           BancoDeDados.carrinhoPreco[indiceAux] = auxiliarPreco[slot];
                           indiceAux++;
                        }
                    }
                    break;
            }
        }
        public static void produto(){
            Scanner leia = new Scanner(System.in);
            int escolha, itens;
            boolean repetir = false;
            String validador;
            while(repetir == false){       
                System.out.println("==================__M E N U__P R O D U T O S__==================");
                System.out.println("Escolha um opção:\n1) Adicionar\t3) Visualizar\n2) Remover\t4) Inicio");
                validador = leia.nextLine();
                if(Validadores.apenasNumeros(validador)){
                    escolha = Integer.parseInt(validador);
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
                            String validadorSub;
                            while(repetirSub == false){
                                int indice = -1;
                                itens = exibirProdutos();
                                System.out.println("\nEscolha o Indice do item que deseja remover.");
                                System.out.printf("Há %s itens na lista.\n",itens);
                                System.out.println("\n================================================================\n");
                                System.out.println("Digite 0 para voltar!!");
                                if(itens > 0){   
                                    validadorSub = leia.nextLine();
                                    if(Validadores.apenasNumeros(validadorSub)){
                                        indice = Integer.parseInt(validadorSub);
                                    }else{
                                        System.out.println("\nDigite apenas numeros!\n");
                                        espera();
                                    }                             
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
                }else{
                    limpa();
                    System.out.println("\nDigite apenas numeros!\n");
                }
            }
        }
        public static void carrinho(){
            Scanner leia = new Scanner(System.in);
            boolean repetir = false;
            int escolha, itens;
            String validador;
            while(repetir == false){
                System.out.println("==================__M E N U__C A R R I N H O__==================");
                System.out.println("Escolha um opção:\n1) Adicionar\t3) Visualizar\n2) Remover\t4) Inicio");
                validador = leia.nextLine();
                if(Validadores.apenasNumeros(validador)){
                    escolha = Integer.parseInt(validador);
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
                            String validadorSub;
                            while(repetirSub == false){
                                int indice = 0;
                                itens = exibirCarrinho();
                                System.out.println("Escolha o Indice do item que deseja remover.");
                                System.out.printf("Há %s itens na lista.\n",itens);
                                System.out.println("\n================================================================\n");
                                System.out.println("Digite 0 para voltar!!");
                                if(itens > 0){   
                                    validadorSub = leia.nextLine();
                                    if(Validadores.apenasNumeros(validadorSub)){
                                        indice = Integer.parseInt(validadorSub);
                                    }else{
                                        System.out.println("\nDigite apenas numeros!\n");
                                    }
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
                }else{
                    limpa();
                    System.out.println("\nDigite apenas numeros!\n");
                }
            }               
        }
        public static void encerrarCompras(){
            Scanner leia = new Scanner(System.in);
            String res = "n";
            boolean repetir = false;
            while(repetir == false){
                do{
                    System.out.println("Itens no carrinho!!");
                    exibirCarrinho();
                    exibirTotal(2);
                    System.out.println("Deseja encerrar as compras? S ou N");
                    if(!apenas_s_ou_n(res)){
                        System.out.println("\nDigite apenas S ou N!\n");
                    }
                    res = leia.nextLine();            
                }while(!apenas_s_ou_n(res));
                if("s".equals(res)){

                }else{
                    repetir = true;
                }
            }
        }
    }

