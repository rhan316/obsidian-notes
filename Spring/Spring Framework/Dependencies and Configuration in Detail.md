
1. Podstawowe typy wartości
	1. value w <property/> lub <construktor-arg/> służy do ustawiania wartości prostych typów (String, int, itd.). Spring konwertuje te wartości na typ właściwości

2. idref element
	1. Umożliwia przekazanie indentyfikatora innego beana jako String (nie referencja). Weryfikuje istnienie beana podczas wdrożenia, zmniejszając ryzyko błędów
```
	<bean id="targetBean" class="..."/>
	<bean id="clientBean" class="...">
		<property name="targetName"><idref bean="targetBean"/></property>
	</bean>
```
3. Referencje do innych beanów (ref):
	1. ref ustawia wartość właściwości jako referencję do innego beana w kontenerze
```
	<property name="myProp"><ref bean="someBean"/></property>
```
4. Inner beans:
	1. Definiowane wewnątrz <property/> lub <construktor-arg/>, bez ID, dostępne tylko w obiektie nadrzędnym
```
	<property name="target">
    <bean class="com.example.Person"><property name="name" value="Fiona"/>  </bean>
</property>

```