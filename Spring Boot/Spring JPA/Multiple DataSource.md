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
```