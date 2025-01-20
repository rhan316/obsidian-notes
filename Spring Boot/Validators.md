Walidatory w Spring Boot służą do sprawdzania poprawności danych wejściowych (np. danych z formularzy, parametrów URL czy ciała żądania w API). Dzięki walidacji możemy upewnić się, że dane wejściowe spełniają określone wymagania, zanim zostaną przetworzone w aplikacji.

***Typy walidatorów w Spring Boot***
1. **Wbudowane adnotacje walidacyjne (Bean Validation).** Takie jak: `@NotNull, @Size, @Email, @NotBlank` itd. Implementowane przez biblioteki takie jak Hibernate Validator.
2. **Własne walidatory (Custom Validators)**. Używane do bardziej zaawansowanych lub niestandardowych reguł walidacyjnych. Wymagają implementacji interfejsu `ConstraintValidator`.
3. **Walidacja ręczna**. Za pomocą klasy `Validator` wbudowanej w Spring, można ręcznie walidować obiekty.

```
@Documented
@Constraint(validatedBy = PhoneNumberValidator.class)
@Target({ElementType.METHOD, ElementType.FIELD})
@Retention(RetentionPolicy.RUNTIME)
public @interface ValidPhoneNumber {
    String message() default "Nieprawidłowy numer telefonu";
    Class<?>[] groups() default {};
    Class<? extends Payload>[] payload() default {};
}


public class PhoneNumberValidator implements ConstraintValidator<ValidPhoneNumber, String> {

    @Override
    public boolean isValid(String phoneNumber, ConstraintValidatorContext context) {
        return phoneNumber != null && phoneNumber.matches("\\+?[0-9]{10,15}");
    }
}

```