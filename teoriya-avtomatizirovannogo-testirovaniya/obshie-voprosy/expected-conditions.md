# Expected conditions

### Таблица `expected_conditions`

| Условие                                  | Когда использовать                              | Пример                                                                            |
| ---------------------------------------- | ----------------------------------------------- | --------------------------------------------------------------------------------- |
| `presence_of_element_located`            | Элемент появился в DOM (но может быть невидим)  | `wait.until(EC.presence_of_element_located((By.ID, "login")))`                    |
| `visibility_of_element_located`          | Элемент появился и видим (ширина/высота > 0)    | `wait.until(EC.visibility_of_element_located((By.ID, "login")))`                  |
| `element_to_be_clickable`                | Элемент доступен для клика (видим и enabled)    | `wait.until(EC.element_to_be_clickable((By.ID, "submit")))`                       |
| `text_to_be_present_in_element`          | Ждать, пока появится нужный текст               | `wait.until(EC.text_to_be_present_in_element((By.ID, "status"), "Готово!"))`      |
| `text_to_be_present_in_element_value`    | Ждать текст внутри value (например, `<input>`)  | `wait.until(EC.text_to_be_present_in_element_value((By.NAME, "q"), "Python"))`    |
| `alert_is_present`                       | Ждать появления alert                           | `wait.until(EC.alert_is_present())`                                               |
| `frame_to_be_available_and_switch_to_it` | Ждать загрузки iframe и переключиться в него    | `wait.until(EC.frame_to_be_available_and_switch_to_it((By.NAME, "frame1")))`      |
| `invisibility_of_element_located`        | Ждать исчезновения элемента                     | `wait.until(EC.invisibility_of_element_located((By.ID, "loader")))`               |
| `element_located_selection_state_to_be`  | Ждать, пока чекбокс станет выбран/снят          | `wait.until(EC.element_located_selection_state_to_be((By.ID, "remember"), True))` |
| `number_of_windows_to_be`                | Ждать, пока откроется нужное количество вкладок | `wait.until(EC.number_of_windows_to_be(2))`                                       |

***

⚡Пример в реальном коде:

```python
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

wait = WebDriverWait(driver, 10)

# Ждать кнопку и кликнуть
button = wait.until(EC.element_to_be_clickable((By.ID, "submit")))
button.click()

# Ждать, пока исчезнет загрузчик
wait.until(EC.invisibility_of_element_located((By.ID, "loader")))
```
