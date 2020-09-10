# Test-selenium

package com.example.tests;

import java.util.regex.Pattern;
import java.util.concurrent.TimeUnit;
import org.testng.annotations.*;
import static org.testng.Assert.*;
import org.openqa.selenium.*;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.openqa.selenium.support.ui.Select;

public class UntitledTestCase {
  private WebDriver driver;
  private String baseUrl;
  private boolean acceptNextAlert = true;
  private StringBuffer verificationErrors = new StringBuffer();

  @BeforeClass(alwaysRun = true)
  public void setUp() throws Exception {
    driver = new FirefoxDriver();
    baseUrl = "https://www.google.com/";
    driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);
  }

  @Test
  public void testUntitledTestCase() throws Exception {
    driver.get("https://corpdemobase.talentrecruit.com/Default.aspx");
    driver.findElement(By.id("TR_Header_rptrHeader_lnkMenu_3")).click();
    driver.findElement(By.id("MainContent_hlnkRegistration")).click();
    driver.findElement(By.id("MainContent_txtEmployeeEmailId")).click();
    driver.findElement(By.id("MainContent_txtEmployeeEmailId")).clear();
    driver.findElement(By.id("MainContent_txtEmployeeEmailId")).sendKeys("adityam.talenetrecruit@gmail.com");
    driver.findElement(By.id("MainContent_txtCaptcha")).click();
    driver.findElement(By.id("MainContent_txtCaptcha")).clear();
    driver.findElement(By.id("MainContent_txtCaptcha")).sendKeys("096354");
    driver.findElement(By.id("MainContent_btnSave")).click();
    driver.findElement(By.xpath("//div[@id='MainContent_divPageContent']/div/div/div[2]/div/div[2]")).click();
    try {
      assertEquals(driver.findElement(By.id("MainContent_lblStatus")).getText(), "We have sent Referral Code to your mail id. Kindly check your mail");
    } catch (Error e) {
      verificationErrors.append(e.toString());
    }
  }

  @AfterClass(alwaysRun = true)
  public void tearDown() throws Exception {
    driver.quit();
    String verificationErrorString = verificationErrors.toString();
    if (!"".equals(verificationErrorString)) {
      fail(verificationErrorString);
    }
  }

  private boolean isElementPresent(By by) {
    try {
      driver.findElement(by);
      return true;
    } catch (NoSuchElementException e) {
      return false;
    }
  }

  private boolean isAlertPresent() {
    try {
      driver.switchTo().alert();
      return true;
    } catch (NoAlertPresentException e) {
      return false;
    }
  }

  private String closeAlertAndGetItsText() {
    try {
      Alert alert = driver.switchTo().alert();
      String alertText = alert.getText();
      if (acceptNextAlert) {
        alert.accept();
      } else {
        alert.dismiss();
      }
      return alertText;
    } finally {
      acceptNextAlert = true;
    }
  }
}
