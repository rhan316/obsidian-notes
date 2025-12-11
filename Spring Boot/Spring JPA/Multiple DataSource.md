Spring nie jest wróżką - on nie znajduje, z której bazy chcesz korzystać.
Musisz zdefiniować każdy DataSource osobno.
Każdy DataSource dostaje swoją własną pulę HikariCP.

Każda baza = osobny DataSource = osobny HikariCP = osobny pool.

### Jak to wygląda?

Masz np.
- bazę główną `primaryDb`
- bazę raportową `reportDb`
Robisz więc:
- `primaryDataSource`
- `reportDataSource`

Każdy z nich to osobny bean:
```java
@Bean
@ConfigurationProperties("spring.datasource.primary")
public DataSource primaryDataSource() {
	return DataSourceBuilder.create().build();
}

@Bean
@ConfigurationProperties("spring.datasource.report")
public DataSource reportDataSource() {
	return DataSourceBuilder.create().build();
}
```

### A co z JPA?

Tutaj zaczynają się schody i ludzie krwawią z nosa.
Bo musisz mieć:
- `EntityManagerFactory` per DataSource
- `TransactionManager` per DataSource
- osobne pakiety z encjami.
![[Pasted image 20251211165142.png]]

![[Pasted image 20251211165228.png]]

