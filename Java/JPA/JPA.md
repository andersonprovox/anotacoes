# JPA

O **JPA** (Java Persistence API) é uma especificação de **ORM** (O rientação de mapa relacional) para resolver o problema de licar com muitas queries de **SQL** em uma aplicação mais complexa. No caso do ecossistema do Java ele aparece para resolver a questão das **Queries** complexas criadas com o **JDBC** e a mudança dos paradigmas de **OOP** e **Entidade relacional**.

Descreve como deve ser o comportamento dos frameworks Java **ORM** que desejarem implementar a sua especificação.

A biblioteca `javax.persistence` possibilita utilizar **classes**, **interfaces** e **annotations** para abstrair o código.

Para persistir os dados com **JPA** deve escolher a implementação que vai executar todo o trabalho.

O **JDBC** é executado por debaixo dos panos.

## Hibernate

O **Hibernate** pode ser usado como ferramenta **ORAM** open source. A Linguagem de consulta orientada a objetos do Hibernate é o **HQL**.

## EclipseLink

O **EclipseLink** é um projeto open source de persistência da Eclipse Foundation. Ele é a Implementação de referência do JPA. Permite os desenvolvedores interagirem com vários serviços de datas. 

A Linguagem de consulta a objetos do EclipseLink é o **EQL**.

## Linguagens de consultas orientadas a objetos

Linguagens criadas para a criação de queries **SQL** usando oconceito de **OOP**.

### JPQL

Linguagem que usa as propriedades de **OOP** para interagir com entidades do **JPA**. Seu uso é mais indicado do que o do entityManager para lidar com alterações de entidades em massa e expressões mais complexas.

### JPA Criteria API

Mais complexa que a **JPQL**, por isso o seu uso deve ser feito em consultas dinâmicas.

Usar **JPQL** e** JPA Criteria API** acaba sendo um desafio em projetos de software, portanto:

- Para consultas simples usar o **JPQL**

- Para consultas mais complexas usar o **JPA Criteria API**

A Eficiência entre as linguagens citadas é equivalente.

### JPA metamodel

Provê a habilidade de examinar o modelo de persistência de um objeto para consultar os detalhes de uma entidade **JPA**. Para cada entidade, uma classe metamodelo é criada com o mesmo nome da classe porém procedido pelo símbolo `_`(underscore) e com os atributos estáticos que representam os campos de persistência.

Usado para referenciar os atributos das entidades e possibilitar o **JPA criteria API** a verificar possíveis erros em tempo de compilação.

Sem este item, os atributos serão referenciados através de Strings tendo como principal desvantagem o risco de ocorrer erro em tempo de excução para o usuário final.

xemplo de como ficaria usando **SQL** Nativo:

```java
String sqlList = "SELECT * FROM aluno";
List<Aluno> alunoSQLList = entityManager.createNativeQuery(sqlList, Aluno.class).getResultList();

//Resultado da lista acima

System.out.println("Consulta alunoSQL" + alunoSQL);
alunoSQLList.forEach(Aluno -> System.out.println("Consulta alunoSQLList: " + Aluno));
```

Usando JPQL:

```java
//trazendo somente um resultado
String jpql = "select a from Aluno a where a.nome = :nome";
Aluno alunoJPQL = entityManager.createQuery(jpql, Aluno.class).setParameter("nome", nome).getSingleResult();

//Trazendo uma lista como resultado
String jpqlList = "select a from Aluno a";
List<Aluno> alunoJPQLList = entityManager.createQuery(jpqlList, Aluno.class).getResultList();
```

Usando JPA Criteria API + JPA metalmodel

```java
CriteriaQuery<Aluno> criteriaQuery = entityManager.getCriteriaBuilder().createQuery(Aluno.class);
```
