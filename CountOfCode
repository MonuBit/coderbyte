import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;

import java.time.Duration;
import java.util.List;

public class BitcoinBlockTest {

    // === Global XPath Constants (Like Android-style central locators) ===
    private static final String BLOCK_URL = "https://blockstream.info/block/000000000000000000076c036ff5119e5a5a74df77abf64203473364509f7732";
    private static final String TX_HEADING_XPATH = "//h2[contains(text(),'Transactions')]";
    private static final String TX_SUBHEADING_XPATH = "//h3[@class="font-h3"]";
    private static final String TRANSACTION_LIST_XPATH = "//div[@id="transaction-box"]";
    private static final String TXID_XPATH = "//div[@class="txn font-p2"]";
    private static final String INPUTS_XPATH = "//div[@class="vin-header-container"]//a";
    private static final String OUTPUTS_XPATH = "//div[@class="vout-header-container"]//a";

    public static void main(String[] args) {
        WebDriver driver = new ChromeDriver();
        WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(15));

        try {
            // Open block page
            driver.get(BLOCK_URL);

            // === Test Case 1: Validate transaction header ===
            WebElement txHeading = wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(TX_HEADING_XPATH)));
            WebElement txSubheading = wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(TX_SUBHEADING_XPATH)));

            if (txSubheading.getText().contains("25 of 2875 Transactions")) {
                System.out.println("✅ Test Case 1 Passed: Correct transaction header found.");
            } else {
                System.out.println("❌ Test Case 1 Failed: Unexpected header text.");
            }

            // === Test Case 2: Parse transactions ===
            List<WebElement> transactions = wait.until(
                    ExpectedConditions.visibilityOfAllElementsLocatedBy(By.xpath(TRANSACTION_LIST_XPATH)));

            System.out.println("✅ Test Case 2: Checking transactions with 1 input and 2 outputs...");
            for (WebElement tx : transactions) {
                String txid = tx.findElement(By.xpath(TXID_XPATH)).getText();
                int inputCount = tx.findElements(By.xpath(INPUTS_XPATH)).size();
                int outputCount = tx.findElements(By.xpath(OUTPUTS_XPATH)).size();

                if (inputCount == 1 && outputCount == 2) {
                    System.out.println("Matching Transaction Hash: " + txid);
                }
            }

        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            driver.quit();
        }
    }
}
