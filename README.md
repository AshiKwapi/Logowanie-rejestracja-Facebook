```package com.mycompany.zadzchatem;

import java.time.Duration;
import java.util.Random;
import org.openqa.selenium.*;//daje dostęp do podstawowych funkcji Selenium, takich jak WebDriver, WebElement, By, itp.
import org.openqa.selenium.edge.EdgeDriver;//umożliwia sterowanie przeglądarką Google Edge
import org.openqa.selenium.support.ui.*;//zawiera pomocnicze klasy, takie jak WebDriverWait i ExpectedConditions. Używamy ich do czekania na określone warunki, takie jak załadowanie strony lub obecność elementu na stronie.

public class Zadzchatem {

    public static void main(String[] args) {

        System.setProperty("webdriver.edge.driver", "src/main/java/msedgedriver.exe"); // Ścieżka do EdgeDrivera

        WebDriver driver = new EdgeDriver();

        try {

            driver.get("https://www.facebook.com/");//wchodzi na stronę docelową

            try {
                Thread.sleep(2000);  // Czeka 2 sekundy
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            WebElement reject = driver.findElement(By.xpath("//*[@id='facebook']/body/div[3]/div[2]/div/div/div/div/div[3]/div[2]/div/div[1]/div[2]/div/div[1]/div/span/span"));//odrzuca pliki cookies
            reject.click();
            WebElement emailField = driver.findElement(By.xpath("//*[@id='email']"));//szuka pola do podania adresu e-mail(na fb można podać maila beż znaku "@" i kontynuacji np."gmail.com"
            emailField.click();
            emailField.sendKeys("Rozalia");//wpisuje swoją nazwę użytkownika

            WebElement passField = driver.findElement(By.xpath("//*[@id='pass']"));//szuka pola do podania hasła
            passField.click();
            passField.sendKeys("Kurczak");//wpisuje hasło
            try {
                Thread.sleep(2000);  // Czeka 2 sekundy
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            WebElement loginField = driver.findElement(By.linkText("Zaloguj się"));//szuka przycisku zaloguj się(tutaj akurat wyszukany po treści tekstu, który jest linkiem bo fb ma zabezpieczenia i po id czasem się nie da) 

            loginField.click();
            try {
                Thread.sleep(2000);  // Czeka 2 sekundy
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

            WebElement goToReg = driver.findElement(By.xpath("//*[@id='login_link']/a[2]"));//dowiaduje się, że nie ma takiego konta, więc szuka elementu, który odniesie go do formularza rejestracyjnego
            goToReg.click();
            try {
                Thread.sleep(2000);  // Czeka 2 sekundy
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

            WebElement Name = driver.findElement(By.xpath("//input[@aria-label='Imię']"));//po kolei szukamy i wypełniamy pola z fomularza
            Name.click();
            Name.sendKeys("Rozalia");
            WebElement Surname = driver.findElement(By.xpath("//input[@aria-label='Nazwisko']"));
            Surname.click();
            Surname.sendKeys("Kuchniak");

            WebElement day = driver.findElement(By.xpath("//select[@aria-label='Dzień']"));
            String day1 = getRandomDay();
            day.sendKeys(day1);
            WebElement month = driver.findElement(By.xpath("//select[@aria-label='Miesiąc']"));
            month.click();
            String month1 = getRandomMonth();
            month.sendKeys(month1);
            WebElement year = driver.findElement(By.xpath("//select[@aria-label='Rok']"));
            year.click();
            String year1 = getRandomYear();
            year.sendKeys(year1);

            WebElement sex = driver.findElement(By.xpath("//label[text()='Kobieta']/input"));
            sex.click();
            WebElement mailornumber = driver.findElement(By.xpath("//input[@aria-label='Numer telefonu komórkowego lub e-mail']"));
            mailornumber.click();
            mailornumber.sendKeys("RozKuchniak123@gmail.com");
            WebElement newPass = driver.findElement(By.xpath("//input[@aria-label='Nowe hasło']"));
            newPass.click();
            newPass.sendKeys("Kurczak");
            try {
                Thread.sleep(2000);  // Czeka 2 sekundy
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            WebElement submitButton = driver.findElement(By.name("websubmit"));//szuka przycisk potwierdzenia rejestracji
            submitButton.click();
            try {
                Thread.sleep(10000);  // Czeka 10 sekund
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

        } catch (Exception e) {
            System.out.println("Błąd: " + e.getMessage());
        } finally {
            // Zamknięcie przeglądarki
            driver.quit();
        }
    }

    public static String getRandomMonth() {
        // Tablica zawierająca skrócone nazwy miesięcy
        String[] months = {"sty", "lut", "mar", "kwi", "maj", "cze", "lip", "sie", "wrz", "paź", "lis", "gru"};

        // Tworzymy obiekt Random
        Random random = new Random();

        // Losujemy indeks tablicy
        int randomIndex = random.nextInt(months.length);

        // Zwracamy losowy miesiąc
        return months[randomIndex];
    }

    public static String getRandomDay() {
        // Tworzymy obiekt Random
        Random random = new Random();

        // Losujemy liczbę z zakresu 1-31
        int randomDay = random.nextInt(31) + 1;  // nextInt(31) daje liczby od 0 do 30, więc dodajemy 1

        // Zwracamy wynik jako String
        return Integer.toString(randomDay);
    }

    public static String getRandomYear() {
        // Tworzymy obiekt Random
        Random random = new Random();

        // Losujemy liczbę z zakresu od 1905 do 2024
        int randomYear = random.nextInt(2024 - 1905 + 1) + 1905; // nextInt(120) daje liczby od 0 do 119, więc dodajemy 1905

        // Zwracamy wynik jako String
        return Integer.toString(randomYear);
    }
}
```
