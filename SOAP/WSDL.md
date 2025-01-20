Plik ***WSDL*** *(Web Services Description Language* to dokument XML, który opisuje interfejs usługi sieciowej SOAP. Określa, jak usługa działa, jakie operacje obsługuje, jakie dane przyjmuje i zwraca, a także gdzie można ją znaleźć (adres endpointu). Jest kluczowym elementem w usługach SOAP, ponieważ pełni rolę kontraktu między klientem a serwerem.

Plik WSDL składa się z kilku kluczowych części:
```
1. `<types>` => Definiuje typy danych, które będą używane w wiadomościach SOAP. Może zawierać schemat XML (XSD) opisujący struktury danych. 

<types>
	<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema">
		<xsd:element name="GetWeatherRequest">
			<xsd:complexType>
				<xsd:sequence>
					<xsd:element name="city" type="xsd:string"/>
					...
```