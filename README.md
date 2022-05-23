Здравствуйте! Ниже будет дано описание классов их полей и методов.

Класс ConvertJson:
Краткое описание: Используется для обработки и сохранения информации из json файлов.
                  Для реализации был использован класс nlohmann::json доступный по
                  адресу: https://github.com/nlohmann/json.
                
 1.Приватные поля:
   а.nlohmann::json config - хранение конфигурации приложения и пути к файлам
                             с информацией из файла config.json;
   b.nlohmann::json requests - хранение пользвательских запросов из файла requests.json;
   c.nlohmann::json answers - хранение резултатов поиска по запросам.

 2.Методы:
   a.ConvertJson - конструктор, выгружает информацию из config.json и requests.json.
                  Вызывает исключени EmptyConfig если конфигурация не заполнена 
                  либо отсутствует, InvalidVersion при несовпадении версий и 
                  NoExistFile если файл не найден. Автоматически заполняет пути файлов,
                  если они не указаны пользователем(только для Windows);
   b.GetResponsesLimit - метод, возвращающий максимальное колличество ответов на запрос(int);
   c.GetRequests - метод, возвращает запросы из файла requests.json(std::vector<std::string>);
   d.putAnswers - метод, выгружает результат работы метода search класса SearchServer в файл answers.json.

Класс InvertedIndex:
Краткое описание: Используется для извлечения слов из документов базы данных и их последующей индексации.

 1.Приватные поля:
   a.freq_dictionary - словарь, хранящий слова, как ключи, и вектор структур Entry, в которых содержатся
                       номер документа и количество слова, содержащегося в ключе.
 2.Методы:
   a.UpdateDocumentBase - обновляет словарь freq_dictionary,
                          принимает на вход список документов для индексации(std::vector<std::string>);
   b.GetWordCount - возвращает вектор структур Entry(std::vector<se::Entry>) для заданного слова. Принимает
                    слово для поиска(std::string)

Класс SearchServer:
Краткое описание: Поиск по заданным документам слов из файла requests.json.

 1.Приватные поля:
   a.index_ - ссылка на класс InvertedIndex.

 2.Методы:
   a.SearchServer - конструктор, принимает ссылку на класс InvertedIndex, инициализирует поле index_;
   b.search - возвращает std::vector<std::vector<RelativeIndex>>, где RelativeIndex - структура, содержащая
              поля doc_id_(номер документа) и rank_(релевантность запроса). Принимает список запросов из файла
              requests.json(const std::vector<std::string>& queries_input).


