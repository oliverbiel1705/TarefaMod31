# JPA

JPA (Java Persistence API) é uma especificação do Java EE (Enterprise Edition) que descreve uma interface comum para frameworks de mapeamento objeto-relacional em Java. Ela define como os objetos Java são mapeados para tabelas em um banco de dados relacional e vice-versa.

Em outras palavras, o JPA permite que você trabalhe com objetos Java em vez de lidar diretamente com consultas SQL e gerenciamento de conexões de banco de dados. Ele fornece uma maneira de representar entidades de domínio (como clientes, produtos, pedidos, etc.) como objetos Java e mapeá-los para as tabelas em um banco de dados relacional de forma transparente.

O principal objetivo do JPA é simplificar o desenvolvimento de aplicativos que fazem uso de banco de dados relacionais, fornecendo uma camada de abstração entre o código Java e o banco de dados subjacente. Isso facilita a manutenção do código, melhora a portabilidade do aplicativo entre diferentes bancos de dados e aumenta a produtividade do desenvolvedor, uma vez que ele pode se concentrar mais na lógica de negócios do que na manipulação de dados.

Frameworks populares que implementam a especificação JPA incluem Hibernate, EclipseLink e OpenJPA. Esses frameworks fornecem implementações concretas da API JPA e adicionam recursos adicionais para facilitar o desenvolvimento de aplicativos Java que interagem com bancos de dados relacionais.

## EXEMPLOS DE ESPECIFICAÇÃO JPA

### Definição de uma Entidade:

Suponha que você tenha uma entidade Produto que deseja mapear para uma tabela no banco de dados:

    import javax.persistence.Entity;
    import javax.persistence.GeneratedValue;
    import javax.persistence.GenerationType;
    import javax.persistence.Id;
    
    @Entity
    public class Produto {
        @Id
        @GeneratedValue(strategy = GenerationType.IDENTITY)
        private Long id;
        private String nome;
        private double preco;
    
        // Construtores, getters e setters
    }
    
### Persistência de uma Entidade:

Com JPA, você pode persistir instâncias de entidades em seu banco de dados de maneira fácil e transparente:

    import javax.persistence.EntityManager;
    import javax.persistence.EntityManagerFactory;
    import javax.persistence.Persistence;
    
    public class Main {
        public static void main(String[] args) {
            EntityManagerFactory emf = Persistence.createEntityManagerFactory("nome-da-unidade-de-persistencia");
            EntityManager em = emf.createEntityManager();
    
            // Criar e persistir uma nova instância de Produto
            em.getTransaction().begin();
            Produto produto = new Produto();
            produto.setNome("Livro de Java");
            produto.setPreco(29.99);
            em.persist(produto);
            em.getTransaction().commit();
    
            em.close();
            emf.close();
        }
    }

### Consultas usando JPA:

Você pode fazer consultas usando JPQL (Java Persistence Query Language), uma linguagem de consulta orientada a objetos similar ao SQL:

    import javax.persistence.Query;
    import java.util.List;
    
    // ...
    
    // Consultar todos os produtos
    em.getTransaction().begin();
    Query query = em.createQuery("SELECT p FROM Produto p");
    List<Produto> produtos = query.getResultList();
    for (Produto p : produtos) {
        System.out.println("ID: " + p.getId() + ", Nome: " + p.getNome() + ", Preço: " + p.getPreco());
    }
    em.getTransaction().commit();