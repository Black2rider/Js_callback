1. Дополни функцию makeMessage так, чтобы она ожидала вторым параметром (параметр callback) колбэк-функцию и возвращала ее вызов. Функция deliverPizza или makePizza будет передаваться как колбэк и ожидать аргументом имя готовой доставляемой пиццы.

        function deliverPizza(pizzaName) {
          return `Доставляем пиццу ${pizzaName}.`;
        }

        function makePizza(pizzaName) {
          return `Пицца ${pizzaName} готовится, ожидайте...`;
        }

        // Пиши код ниже этой строки
        function makeMessage(pizzaName, callback) {
          return callback(pizzaName);
        }



2. Задание
Необходимо написать логику обработки заказа пиццы. Выполни рефакторинг метода order так, чтобы он принимал вторым и третим параметрами два колбэка onSuccess и onError.

Если в свойстве pizzas нет пиццы с названием из параметра pizzaName, метод order должен возвращать результат вызова колбэка onError, передавая ему аргументом строку 'В ассортименте нет пиццы с названием <имя пиццы>.'
Если в свойстве pizzas есть пицца с названием из параметра pizzaName, метод order должен возвращать результат вызова колбэка onSuccess, передавая ему аргументом имя заказанной пиццы.

          const pizzaPalace = {
            pizzas: ['Ультрасыр', 'Аль Копчино', 'Четыре нарезона'],
            order(pizzaName, makePizza, onOrderError) {
            if (this.pizzas.includes(pizzaName)) {
              return makePizza(pizzaName);
            } 
              return onOrderError(`В ассортименте нет пиццы с названием ${pizzaName}.`);
            },
          }
          // Пиши код выше этой строки

          // Колбэк для onSuccess
          function makePizza(pizzaName) {
            return `Ваш заказ принят. Готовим пиццу ${pizzaName}.`;
          }

          // Колбэк для onError
          function onOrderError(error) {
            return `Ошибка! ${error}`;
          }

          // Вызовы метода с колбэками
          pizzaPalace.order('Аль Копчино', makePizza, onOrderError);
          pizzaPalace.order('Четыре нарезона', makePizza, onOrderError);
          pizzaPalace.order('Биг майк', makePizza, onOrderError);
          pizzaPalace.order('Венская', makePizza, onOrderError);



3. Тесты
Объявлена переменная customer.
Значение переменной customer это объект со свойствами и методами.
Вызов customer.getDiscount() возвращает текущее значение свойства discount.
Вызов customer.setDiscount(0.15) обновляет значение свойства discount.
Вызов customer.getBalance() возвращает текущее значение свойства balance.
Вызов customer.getOrders() возвращает текущее значение свойства orders.
Вызов customer.addOrder(5000, 'Steak') добавляет 'Steak' в массив значений свойства orders и обновляет баланс.
Метод getBalance объекта customer использует this.
Метод getDiscount объекта customer использует this.
Метод setDiscount объекта customer использует this.
Метод getOrders объекта customer использует this.
Метод addOrder объекта customer использует this.

        const customer = {
          username: 'Mango',
          balance: 24000,
          discount: 0.1,
          orders: ['Burger', 'Pizza', 'Salad'],
          // Пиши код ниже этой строки
          getBalance() {
            return this.balance;
          },
          getDiscount() {
            return this.discount;
          },
          setDiscount(value) {
            this.discount = value;
          },
          getOrders() {
            return this.orders;
          },
          addOrder(cost, order) {
            this.balance -= cost - cost * this.discount;
            this.orders.push(order);
          },
          // Пиши код выше этой строки
        };

        customer.setDiscount(0.15);
        console.log(customer.getDiscount()); // 0.15
        customer.addOrder(5000, 'Steak');
        console.log(customer.getBalance()); // 19750
        console.log(customer.getOrders()); // ['Burger', 'Pizza', 'Salad', 'Steak']



4. Задание
Сервису приготовления и доставки еды требуется функция генерации сообщений о статусе заказа.

Дополни функцию composeMessage(position) так, чтобы она возвращала строку в формате 'Готовим <блюдо> для <почта>. Ваш заказ <позиция>-й в очереди.' Позиция это значение параметра position - позиция элемента в массиве (на единицу больше чем индекс).

Не объявляй дополнительные параметры функции composeMessage(position).
Используй call для вызова функции в контексте одного объекта-заказа.
Используй this в теле функции для доступа к свойствам объекта-заказа в контексте которого она была вызывана.
Дополни код так, чтобы в переменной messages получился массив сообщений о статусе заказов из массива orders с помощью цикла for.

          const orders = [
            { email: 'solomon@topmail.ua', dish: 'Burger' },
            { email: 'artemis@coldmail.net', dish: 'Pizza' },
            { email: 'jacob@mail.com', dish: 'Taco' },
          ];

          // Пиши код ниже этой строки
          function composeMessage(position) {
           return `Готовим ${this.dish} для ${this.email}. Ваш заказ ${position +=  1}-й в очереди.`;
          }

          const messages = [];

          for (let i = 0; i < Object.keys(orders).length; i += 1) {
            messages.push(composeMessage.call(orders[i], i))
          }
