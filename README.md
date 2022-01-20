![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=java&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-005C84?style=for-the-badge&logo=mysql&logoColor=white)

## Projeto Java , MySQL , DAO , JDBC
Projeto Java , MySQL , DAO (Data Access Objects), JDBC

### Estudando Java , MySQL , DAO (Data Access Objects), JDBC (Java Database Connectivity)

> (( em andamento ))

<p align="center">
        <a href="https://www.linkedin.com/in/allan-pereira-abrahao/">
        <img align="center" width="525" height="171"  src="/img-readme/uml1.png" />
</a>
</p>

### Exemplo de conexão e requisição
```java
@Override
	public Seller findById(Integer id) {
		PreparedStatement st = null;
		ResultSet rs = null;
		try {
			st = conn.prepareStatement(
					"SELECT seller.*,department.Name as DepName "
					+ "FROM seller INNER JOIN department "
					+ "ON seller.DepartmentId = department.Id "
					+ "WHERE seller.Id = ?");

			st.setInt(1, id);
			rs = st.executeQuery();
			if (rs.next()) {
				Department dep = instantiateDepartment(rs);
				Seller seller = instantiateSeller(rs, dep);
				return seller;
			}
			return null;
		}
		catch (SQLException e) {
			throw new DbException(e.getMessage());
		}
		finally {
			DB.closeStatement(st);
			DB.closeResultSet(rs);
		}
	}
```

### Exemplo de requisição de todos os usuários de determinado departamento, neste caso o 2
```java
System.out.println("\n=== TEST 2: seller findByDepartment =====");
		Department department = new Department(2, null);
		List<Seller> list = sellerDao.findByDepartment(department);
		for (Seller obj : list) {
			System.out.println(obj);
		}
```
### Retorno ( ver arquivos json exportados do banco de dados /arquivos-json-db abaixo exemplo )
```java
Seller [id=6, name=Alex Pink, email=bob@gmail.com, birthDate=1997-03-04, baseSalary=3090.0, department=Department [id=2, name=Electronics]]
Seller [id=2, name=Maria Green, email=maria@gmail.com, birthDate=1979-12-31, baseSalary=3090.0, department=Department [id=2, name=Electronics]]
```

### DB exportados em json
```json
[
    {
        "Id": 1,
        "Name": "Bob Brown",
        "Email": "bob@gmail.com",
        "BirthDate": "1998-04-21 00:00:00",
        "BaseSalary": 1000.0,
        "DepartmentId": 1
    },
    {
        "Id": 2,
        "Name": "Maria Green",
        "Email": "maria@gmail.com",
        "BirthDate": "1979-12-31 00:00:00",
        "BaseSalary": 3090.0,
        "DepartmentId": 2
    },
    {
        "Id": 3,
        "Name": "Alex Grey",
        "Email": "alex@gmail.com",
        "BirthDate": "1988-01-15 00:00:00",
        "BaseSalary": 1000.0,
        "DepartmentId": 1
    },
    {
        "Id": 4,
        "Name": "Martha Red",
        "Email": "martha@gmail.com",
        "BirthDate": "1993-11-30 00:00:00",
        "BaseSalary": 3000.0,
        "DepartmentId": 4
    },
    {
        "Id": 5,
        "Name": "Donald Blue",
        "Email": "donald@gmail.com",
        "BirthDate": "2000-01-09 00:00:00",
        "BaseSalary": 4000.0,
        "DepartmentId": 3
    },
    {
        "Id": 6,
        "Name": "Alex Pink",
        "Email": "bob@gmail.com",
        "BirthDate": "1997-03-04 00:00:00",
        "BaseSalary": 3090.0,
        "DepartmentId": 2
    },
    {
        "Id": 7,
        "Name": "Carl Purple",
        "Email": "carl@gmail.com",
        "BirthDate": "1985-04-22 00:00:00",
        "BaseSalary": 3000.0,
        "DepartmentId": 4
    }
]
```

#### Agradecimentos ao Professor [Nélio Alves](https://devsuperior.com.br)