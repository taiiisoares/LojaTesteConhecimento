# LojaTesteConhecimento
Esse projeto é voltado para o teste de conhecimentos técnicos em Desenvolvimento de Sistemas.
    
    package loja.aprimorada;   
        public static boolean apenasLetras(String cadeia){
            boolean teste = cadeia.matches("(?i)(?x)[A-Z]+");
            return teste;
        }
        public static boolean apenasNumeros(String cadeia){
            boolean teste = cadeia.matches("[0-9.]+");
            return teste;
        }
        public static boolean apenas_s_ou_n(String cadeia){
            boolean teste = cadeia.matches("(?i)[s,n]");
            return teste;
        }
    }
