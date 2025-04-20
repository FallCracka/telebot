from telebot import types
import telebot
import random
import os

# Получаем токен из переменной окружения

TOKEN = os.getenv("TOKEN")


# Инициализируем бота

bot = telebot.TeleBot(TOKEN)


correct_answer = ''
user_answer = ''
score = 0
a = 1
n = 0
facts = ['Уильям Шекспир изобрел около 1700 новых слов, включая такие термины, как "грустный" и "сумасшедший"',
             'Самым продаваемым романом всех времен является "Маленький принц" Антуана де Сент-Экзюпери, переведенный на более чем 250 языков.',
             '"Горе от ума" Александра Грибоедова изначально было написано в стихах, но позже адаптировано в прозу.',
             'Лев Толстой отказался от Нобелевской премии мира в 1901 году, считая себя недостойным этой награды.',
             '"Моби Дик" Германа Мелвилла был первоначально опубликован как сериал в журнале.',
             'Федор Достоевский написал роман "Преступление и наказание" всего за 26 дней.',
             '"Алиса в Стране чудес" Льюиса Кэрролла была вдохновлена реальной девочкой по имени Алиса Лидделл.',
             'Джейн Остин начала писать романы в возрасте 12 лет.',
             '"Война и мир" Льва Толстого содержит более 500 персонажей.',
             'Эрнест Хемингуэй однажды выиграл пари, написав самый короткий рассказ: "For sale: baby shoes, never worn."',
             '"Повелитель мух" Уильяма Голдинга был отвергнут 21 издателем перед публикацией.',
             'Франц Кафка просил своего друга уничтожить все его рукописи после смерти, но тот нарушил его волю.',
             '"Мастер и Маргарита" Михаила Булгакова был опубликован посмертно, спустя 27 лет после завершения работы над романом.',
             'Джеймс Джойс потратил 17 лет на создание романа "Улисс".',
             '"1984" Джорджа Оруэлла был написан в 1948 году, но название получилось путем перестановки последних двух цифр года написания.',
             '"Приключения Гулливера" Джонатана Свифта были написаны как сатира на человеческое общество.',
             'Владимир Набоков написал "Лолиту" на английском языке, хотя русский был его родным языком.',
             '"Гарри Поттер" Джоан Роулинг был отклонен 12 издательствами, прежде чем был принят Bloomsbury.',
             'Александр Пушкин писал стихи даже во время дуэлей.',
            'Самая длинная книга: Роман Марселя Пруста «В поисках утраченного времени» состоит из семи томов и содержит около 1,5 миллионов слов. Это одна из самых длинных книг в мировой литературе.',
         'Самый короткий рассказ: Рассказ Эрнеста Хемингуэя, состоящий всего из шести слов: «For sale: baby shoes, never worn» («Продаются детские ботинки, неношеные»). Этот минирассказ передает целую гамму эмоций и сюжетов.',
         'Первая печатная книга: Считается, что первой напечатанной книгой была Библия, известная как Библия Гутенберга, изданная Иоганном Гутенбергом в середине XV века. Эта технология печати произвела революцию в распространении знаний.',
         'Литературные мистификации: Некоторые авторы использовали псевдонимы для публикации своих произведений. Например, Джейн Остин публиковала свои ранние работы анонимно, чтобы избежать предвзятости читателей к женским авторам.',
         'Интерактивная литература: В последние годы популярность набирает интерактивная литература, где читатель сам выбирает развитие сюжета. Одним из примеров является серия книг «Выбери свое приключение».']
# Основные команды

"""" Обработчик команды /start"""

@bot.message_handler(commands=['start'])
def start(message):
    markup = types.InlineKeyboardMarkup()
    rec_but = types.InlineKeyboardButton('Рекомендации по жанрам', callback_data='recomend_callback')
    markup.row(rec_but)
    quiz_but = types.InlineKeyboardButton('Решить квиз', callback_data='quiz_callback')
    fact_but = types.InlineKeyboardButton('Интересные факты', callback_data='fact_callback')
    markup.row(quiz_but, fact_but)
    bot.send_message(message.chat.id, text='Привет, {message.from_user.username}! Этот бот создан для того, чтобы получить полезную информацию и просто развлечься.', reply_markup=markup)


""" Кнопка 'Главное меню' """

@bot.callback_query_handler(func=lambda call: call.data == 'back_to_main')
def back_to_main_menu(callback):
    global a, score
    score = 0
    a = 1
    markup = types.InlineKeyboardMarkup()
    rec_but = types.InlineKeyboardButton('Рекомендации по жанрам', callback_data='recomend_callback')
    markup.row(rec_but)
    quiz_but = types.InlineKeyboardButton('Решить квиз', callback_data='quiz_callback')
    fact_but = types.InlineKeyboardButton('Интересные факты', callback_data='fact_callback')
    markup.row(quiz_but, fact_but)
    bot.edit_message_text(chat_id=callback.message.chat.id, message_id=callback.message.id, text=f'Привет, {callback.from_user.username}! Этот бот создан для того, чтобы получить полезную информацию и просто развлечься.', reply_markup=markup)


# Раздел рекомендации по жанрам

""" Кнопка 'Рекомендации по жанрам' """

@bot.callback_query_handler(func=lambda call: call.data == 'recomend_callback')
def recomendation(callback):
    markup = types.InlineKeyboardMarkup()
    romance_but = types.InlineKeyboardButton('Роман', callback_data='romance_callback')
    story_but = types.InlineKeyboardButton('Рассказ', callback_data='story_callback')
    narrative_but = types.InlineKeyboardButton('Повесть', callback_data='narrative_callback')
    tale_but = types.InlineKeyboardButton('Сказка', callback_data='tale_callback')
    tragedy_but = types.InlineKeyboardButton('Трагедия', callback_data='tragedy_callback')
    comedy_but = types.InlineKeyboardButton('Комедия', callback_data='comedy_callback')
    drama_but = types.InlineKeyboardButton('Драма', callback_data='drama_callback')
    main_menu_but = types.InlineKeyboardButton('Главное меню', callback_data='back_to_main')
    markup.row(romance_but, story_but, narrative_but, tale_but)
    markup.row(tragedy_but, comedy_but, drama_but)
    markup.row(main_menu_but)
    bot.edit_message_text(chat_id=callback.message.chat.id, message_id=callback.message.id, text='<b>Вы выбрали рекомендации по жанрам</b> \n \n Выберите жанр:', reply_markup=markup, parse_mode='html')


""" Кнопка 'Роман' """

@bot.callback_query_handler(func=lambda call: call.data == 'romance_callback')
def romance(callback):
    markup = types.InlineKeyboardMarkup()
    main_menu_but = types.InlineKeyboardButton('Главное меню', callback_data='back_to_main')
    back_but = types.InlineKeyboardButton('Назад', callback_data='back_recomend_callback')
    markup.row(main_menu_but, back_but)
    bot.edit_message_text(chat_id=callback.message.chat.id, message_id=callback.message.id, text='<b>Вы выбрали рекомендации в жанре Роман</b> \n \n'
                                                                                                 '<b>1. "Война и мир" Лев Толстой</b> \n'
                                                                                                 'Эпический роман о жизни русского общества начала XIX века, переплетающий судьбы множества персонажей с историческими событиями, такими как Отечественная война 1812 года.\n \n'
                                                                                                 '<b>2. "Анна Каренина" Лев Толстой</b> \n'
                                                                                                 'Глубокий психологический роман о любви, предательстве и страданиях, ставший одним из величайших произведений русской литературы.\n \n'
                                                                                                 '<b>3. "Мастер и Маргарита" Михаил Булгаков</b> \n'
                                                                                                 'Фантастически-реалистическое произведение, где магия и сатира сочетаются с философскими размышлениями о добре и зле, власти и свободе.\n \n'
                                                                                                 '<b>4. "Сто лет одиночества" Габриэль Гарсиа Маркес</b> \n'
                                                                                                 'Магический реализм в чистом виде: история семьи Буэндиа, которая живет в вымышленном городе Макондо, переплетается с историей Латинской Америки.\n \n'
                                                                                                 '<b>5. "Улисс" Джеймс Джойс</b> \n'
                                                                                                 'Экспериментальный роман, который считается вершиной модернизма. Описывает один день из жизни дублинского еврея Леопольда Блума и его жены Молли.', reply_markup=markup, parse_mode='html')

""" Кнопка 'Рассказ' """

@bot.callback_query_handler(func=lambda call: call.data == 'story_callback')
def story(callback):
    markup = types.InlineKeyboardMarkup()
    main_menu_but = types.InlineKeyboardButton('Главное меню', callback_data='back_to_main')
    back_but = types.InlineKeyboardButton('Назад', callback_data='back_recomend_callback')
    markup.row(main_menu_but, back_but)
    bot.edit_message_text(chat_id=callback.message.chat.id, message_id=callback.message.id, text='<b>Вы выбрали рекомендации в жанре Рассказ</b> \n \n'
                                                                                                 '<b>1. "Превращение" Франца Кафки</b> \n'
                                                                                                 'Этот рассказ считается одним из шедевров мировой литературы. История о человеке, который просыпается и обнаруживает, что превратился в огромное насекомое, исследует темы отчуждения, абсурда и человеческой природы.\n \n'
                                                                                                 '<b>2. "Кроткие" Федора Достоевского</b> \n'
                                                                                                 'Глубокий психологический рассказ, в котором Достоевский исследует внутренние переживания женщины, переживающей трагедию. Это произведение поражает своей эмоциональной насыщенностью и глубиной.\n \n'
                                                                                                 '<b>3. "Смерть Ивана Ильича" Льва Толстого</b> \n'
                                                                                                 'Рассказ о жизни и смерти, в котором Толстой мастерски передает внутренние переживания человека, осознающего неизбежность конца. Это произведение о смысле жизни и о том, как мы относимся к смерти.\n \n'
                                                                                                 '<b>4. "Судьба человека" Михаила Шолохова</b> \n'
                                                                                                 'Эмоционально насыщенный рассказ о судьбе солдата, потерявшего семью во время войны. Произведение затрагивает темы мужества, стойкости и человеческой выносливости.\n \n'
                                                                                                 '<b>5. "Старуха Изергиль" Максима Горького</b> \n'
                                                                                                 'Рассказ, в котором Горький исследует темы свободы, любви и судьбы. Это произведение сочетает в себе элементы легенды и реальности, создавая уникальную атмосферу.', reply_markup=markup, parse_mode='html')



""" Кнопка 'Повесть' """

@bot.callback_query_handler(func=lambda call: call.data == 'narrative_callback')
def narrative(callback):
    markup = types.InlineKeyboardMarkup()
    main_menu_but = types.InlineKeyboardButton('Главное меню', callback_data='back_to_main')
    back_but = types.InlineKeyboardButton('Назад', callback_data='back_recomend_callback')
    markup.row(main_menu_but, back_but)
    bot.edit_message_text(chat_id=callback.message.chat.id, message_id=callback.message.id, text='<b>Вы выбрали рекомендации в жанре Повесть</b> \n \n'
                                                                                                 '<b>1. "Повелитель мух" Уильяма Голдинга</b> \n'
                                                                                                 'Эта повесть исследует природу человека и общества через призму выживания группы мальчиков на необитаемом острове. Произведение считается классикой антиутопической литературы.\n \n'
                                                                                                 '<b>2. "Старик и море" Эрнеста Хемингуэя</b> \n'
                                                                                                 'История о старике-сантере, который борется с гигантским марлином в открытом море, стала символом стойкости и мужества. Повесть принесла Хемингуэю Нобелевскую премию по литературе.\n \n'
                                                                                                 '<b>3. "О дивный новый мир" Олдоса Хаксли</b> \n'
                                                                                                 'Антиутопическая повесть, в которой Хаксли описывает общество будущего, где счастье достигается через контроль и манипуляции. Произведение поднимает вопросы о свободе, индивидуальности и человеческом достоинстве.\n \n'
                                                                                                 '<b>4. "Повесть о настоящем человеке" Бориса Полевого</b> \n'
                                                                                                 'Советская повесть, основанная на реальных событиях, рассказывает о летчике Алексее Маресьеве, который, потеряв обе ноги, возвращается в строй и продолжает сражаться. Произведение стало символом мужества и стойкости.\n \n'
                                                                                                 '<b>5. "Ночь нежна" Фрэнсиса Скотта Фицджеральда</b> \n'
                                                                                                 'Эта повесть исследует темы любви, богатства и разрушения. История о молодом психиатре и его богатой пациентке, разворачивающаяся на фоне роскошной жизни на Лазурном берегу, сочетает в себе романтику и трагедию.', reply_markup=markup, parse_mode='html')

""" Кнопка 'Сказка' """

@bot.callback_query_handler(func=lambda call: call.data == 'tale_callback')
def tale(callback):
    markup = types.InlineKeyboardMarkup()
    main_menu_but = types.InlineKeyboardButton('Главное меню', callback_data='back_to_main')
    back_but = types.InlineKeyboardButton('Назад', callback_data='back_recomend_callback')
    markup.row(main_menu_but, back_but)
    bot.edit_message_text(chat_id=callback.message.chat.id, message_id=callback.message.id, text='<b>Вы выбрали рекомендации в жанре Сказка</b> \n \n'
                                                                                                 '<b>1. "Маленький принц" Антуана де Сент-Экзюпери</b> \n'
                                                                                                 'Эта философская сказка о маленьком принце, путешествующем по разным планетам, исследует темы дружбы, любви и смысла жизни. Произведение наполнено глубокими мыслями, которые заставляют задуматься о важных вещах.\n \n'
                                                                                                 '<b>2. "Алиса в Стране Чудес" Льюиса Кэрролла</b> \n'
                                                                                                 'Классическая сказка о девочке Алисе, которая попадает в странный и волшебный мир, полный абсурда и необычных персонажей. Произведение стало символом детской литературы и вдохновило множество адаптаций.\n \n'
                                                                                                 '<b>3. "Волшебник Изумрудного города" Александра Волкова</b> \n'
                                                                                                 'Советская интерпретация истории о девочке Элли и ее друзьях, которые отправляются в путешествие по волшебной стране в поисках исполнения своих желаний. Произведение стало культовым в России и странах СНГ.\n \n'
                                                                                                 '<b>4. "Пиноккио" Карло Коллоди</b> \n'
                                                                                                 'История о деревянном мальчике, который мечтает стать настоящим, учит нас важности честности и доброты. Сказка полна приключений и моральных уроков, которые остаются актуальными и сегодня.\n \n'
                                                                                                 '<b>5. "Хоббит, или Туда и обратно" Дж. Р. Р. Толкина</b> \n'
                                                                                                 'Приключенческая сказка о хоббите Бильбо Бэггинсе, который отправляется в путешествие вместе с гномами и волшебником Гэндальфом. Произведение стало основой для создания вселенной "Властелина колец" и вдохновило множество фэнтези-авторов.', reply_markup=markup, parse_mode='html')


""" Кнопка 'Трагедия' """

@bot.callback_query_handler(func=lambda call: call.data == 'tragedy_callback')
def tragedy(callback):
    markup = types.InlineKeyboardMarkup()
    main_menu_but = types.InlineKeyboardButton('Главное меню', callback_data='back_to_main')
    back_but = types.InlineKeyboardButton('Назад', callback_data='back_recomend_callback')
    markup.row(main_menu_but, back_but)
    bot.edit_message_text(chat_id=callback.message.chat.id, message_id=callback.message.id, text='<b>Вы выбрали рекомендации в жанре Трагедия</b> \n \n'
                                                                                                 '<b>1. "Гамлет" Уильяма Шекспира</b> \n'
                                                                                                 'Одна из самых известных трагедий в мировой литературе, "Гамлет" рассказывает историю принца Датского, который пытается отомстить за убийство своего отца. Произведение исследует темы мести, безумия и человеческой природы.\n \n'
                                                                                                 '<b>2. "Царь Эдип" Софокла</b> \n'
                                                                                                 'Древнегреческая трагедия, в которой царь Эдип, пытаясь избежать предсказанной судьбы, невольно становится ее жертвой. Произведение исследует темы судьбы, вины и моральной ответственности.\n \n'
                                                                                                 '<b>3. "Фауст" Иоганна Вольфганга Гёте</b> \n'
                                                                                                 'Трагедия о ученом, который продает свою душу дьяволу в обмен на знания и власть. Произведение исследует темы морали, науки и человеческой жадности.\n \n'
                                                                                                 '<b>4. "Отелло" Уильяма Шекспира</b> \n'
                                                                                                 'История о ревнивом венецианском генерале, который под влиянием злодея Яго убивает свою жену Дездемону. Трагедия исследует темы ревности, доверия и предательства.\n \n'
                                                                                                 '<b>5. "Король Лир" Уильяма Шекспира</b> \n'
                                                                                                 'Трагедия о стареющем короле, который разделяет свое королевство между двумя из трех дочерей, что приводит к катастрофическим последствиям. Произведение исследует темы власти, семьи и безумия.', reply_markup=markup, parse_mode='html')


""" Кнопка 'Комедия' """

@bot.callback_query_handler(func=lambda call: call.data == 'comedy_callback')
def comedy(callback):
    markup = types.InlineKeyboardMarkup()
    main_menu_but = types.InlineKeyboardButton('Главное меню', callback_data='back_to_main')
    back_but = types.InlineKeyboardButton('Назад', callback_data='back_recomend_callback')
    markup.row(main_menu_but, back_but)
    bot.edit_message_text(chat_id=callback.message.chat.id, message_id=callback.message.id, text='<b>Вы выбрали рекомендации в жанре Комедия</b> \n \n'
                                                                                                 '<b>1. "Дон Кихот" Мигеля де Сервантеса</b> \n'
                                                                                                 'История о рыцаре, который, вдохновленный романами о рыцарях, отправляется в путешествие, чтобы совершить подвиги. Произведение сочетает в себе юмор, сатиру и философские размышления.\n \n'
                                                                                                 '<b>2. "Тартюф" Мольера</b> \n'
                                                                                                 'Комедия о лицемере, который пытается обмануть доверчивого хозяина дома. Произведение высмеивает лицемерие и обман, а также исследует темы морали и общества.\n \n'
                                                                                                 '<b>3. "Мертвые души" Николая Гоголя</b> \n'
                                                                                                 'Сатирическая поэма в прозе, в которой главный герой путешествует по России, покупая "мертвые души" — крепостных крестьян, которые уже умерли, но еще не вычеркнуты из ревизских списков. Произведение высмеивает пороки российского общества.\n \n'
                                                                                                 '<b>4. "В ожидании Годо" Сэмюэля Беккета</b> \n'
                                                                                                 'Абсурдистская пьеса о двух бродягах, которые ждут таинственного Годо. Произведение исследует темы бессмысленности и абсурда жизни, но делает это с юмором и иронией.\n \n'
                                                                                                 '<b>5. "Пигмалион" Джорджа Бернарда Шоу</b> \n'
                                                                                                 'Комедия о профессоре фонетики, который делает ставку, что сможет превратить цветочницу в леди. Произведение сочетает в себе юмор и социальные комментарии.', reply_markup=markup, parse_mode='html')


""" Кнопка 'Драма' """

@bot.callback_query_handler(func=lambda call: call.data == 'drama_callback')
def drama(callback):
    markup = types.InlineKeyboardMarkup()
    main_menu_but = types.InlineKeyboardButton('Главное меню', callback_data='back_to_main')
    back_but = types.InlineKeyboardButton('Назад', callback_data='back_recomend_callback')
    markup.row(main_menu_but, back_but)
    bot.edit_message_text(chat_id=callback.message.chat.id, message_id=callback.message.id, text='<b>Вы выбрали рекомендации в жанре Драма</b> \n \n'
                                                                                                 '<b>1. "Гамлет" Уильяма Шекспира</b> \n'
                                                                                                 'Трагедия о принце Датском, который пытается отомстить за убийство своего отца, исследует темы мести, безумия и человеческой природы. Произведение считается одной из величайших драм в мировой литературе.\n \n'
                                                                                                 '<b>2. "Царь Эдип" Софокла</b> \n'
                                                                                                 'Древнегреческая трагедия, в которой царь Эдип, пытаясь избежать предсказанной судьбы, невольно становится ее жертвой. Произведение исследует темы судьбы, вины и моральной ответственности.\n \n'
                                                                                                 '<b>3. "Фауст" Иоганна Вольфганга Гёте</b> \n'
                                                                                                 'Трагедия о ученом, который продает свою душу дьяволу в обмен на знания и власть. Произведение исследует темы морали, науки и человеческой жадности.\n \n'
                                                                                                 '<b>4. "Отелло" Уильяма Шекспира</b> \n'
                                                                                                 'История о ревнивом венецианском генерале, который под влиянием злодея Яго убивает свою жену Дездемону. Трагедия исследует темы ревности, доверия и предательства.\n \n'
                                                                                                 '<b>5. "Король Лир" Уильяма Шекспира</b> \n'
                                                                                                 'Трагедия о стареющем короле, который разделяет свое королевство между двумя из трех дочерей, что приводит к катастрофическим последствиям. Произведение исследует темы власти, семьи и безумия.', reply_markup=markup, parse_mode='html')
""" Кнопка 'Назад'"""

@bot.callback_query_handler(func=lambda call: call.data == 'back_recomend_callback')
def recomend_back_callback(callback):
    markup = types.InlineKeyboardMarkup()
    romance_but = types.InlineKeyboardButton('Роман', callback_data='romance_callback')
    story_but = types.InlineKeyboardButton('Рассказ', callback_data='story_callback')
    narrative_but = types.InlineKeyboardButton('Повесть', callback_data='narrative_callback')
    tale_but = types.InlineKeyboardButton('Сказка', callback_data='tale_callback')
    tragedy_but = types.InlineKeyboardButton('Трагедия', callback_data='tragedy_callback')
    comedy_but = types.InlineKeyboardButton('Комедия', callback_data='comedy_callback')
    drama_but = types.InlineKeyboardButton('Драма', callback_data='drama_callback')
    main_menu_but = types.InlineKeyboardButton('Главное меню', callback_data='back_to_main')
    markup.row(romance_but, story_but, narrative_but, tale_but)
    markup.row(tragedy_but, comedy_but, drama_but)
    markup.row(main_menu_but)
    bot.edit_message_text(chat_id=callback.message.chat.id, message_id=callback.message.id, text='<b>Вы выбрали рекомендацию по жанрам</b> \n \n Выберите жанр:', reply_markup=markup, parse_mode='html')


# Раздел "Квиз"


""" Кнопка квиз"""

@bot.callback_query_handler(func=lambda call: call.data == 'quiz_callback')
def quiz_main_callback(callback):
    markup = types.InlineKeyboardMarkup()
    quiz_but1 = types.InlineKeyboardButton('Квиз 1', callback_data='quiz1_callback')
    quiz_but2 = types.InlineKeyboardButton('Квиз 2', callback_data='quiz2_callback')
    main_menu_but = types.InlineKeyboardButton('Главное меню', callback_data='back_to_main')
    markup.row(quiz_but1, quiz_but2)
    markup.row(main_menu_but)
    bot.edit_message_text(chat_id=callback.message.chat.id, message_id=callback.message.id, text='<b>Вы выбрали Квиз</b> \n \nВыберите квиз:', reply_markup=markup, parse_mode='html')


""" Кнопка 'Квиз 1' """

@bot.callback_query_handler(func=lambda call: call.data == 'quiz1_callback')
def quiz1_callback(callback):
    global user_answer, correct_answer, a, n
    n = 1
    markup = types.InlineKeyboardMarkup()
    first = types.InlineKeyboardButton('1', callback_data='answer_1')
    second = types.InlineKeyboardButton('2', callback_data='answer_2')
    third = types.InlineKeyboardButton('3', callback_data='answer_3')
    markup.row(first, second, third)
    next_quest = types.InlineKeyboardButton('Следующий вопрос', callback_data='next1_quest')
    markup.row(next_quest)
    main_menu_but = types.InlineKeyboardButton('Главное меню', callback_data='back_to_main')
    back_but = types.InlineKeyboardButton('К выбору квиза', callback_data='back_quiz_callback')
    markup.row(main_menu_but, back_but)
    while a > 0:
        if a == 1:
            bot.edit_message_text(chat_id=callback.message.chat.id, message_id=callback.message.id,
                              text=f'<b>Вы выбрали Квиз №{n} (Вопрос {a})</b> \n \n<b>Кто является автором романа "Мастер и Маргарита"?</b> \n \n1) Лев Толстой 2) Михаил Булгаков 3) Федор Достоевский',
                              reply_markup=markup, parse_mode='html')
            correct_answer = 2
        elif a == 2:
            bot.edit_message_text(chat_id=callback.message.chat.id, message_id=callback.message.id,
                              text=f'<b>Вы выбрали Квиз №{n} (Вопрос {a})</b> \n \n<b>Как зовут главного героя романа Льва Толстого "Война и мир"?</b> \n \n1) Андрей Болконский 2) Пьер Безухов 3) Наташа Ростова',
                              reply_markup=markup, parse_mode='html')
            correct_answer = 2
        elif a == 3:
            bot.edit_message_text(chat_id=callback.message.chat.id, message_id=callback.message.id,
                              text=f'<b>Вы выбрали Квиз №{n} (Вопрос {a})</b> \n \n<b>Какое прозвище было у Тараса Бульбы, героя одноименной повести Николая Гоголя?</b> \n \n1) Запорожец 2) Старый казак 3) Тарас-воин',
                              reply_markup=markup, parse_mode='html')
            correct_answer = 3
        else:
            result_quest(callback)


""" Кнопка 'Квиз 2' """

@bot.callback_query_handler(func=lambda call: call.data == 'quiz2_callback')
def quiz2_callback(callback):
    global user_answer, correct_answer, a, n
    n = 2
    markup = types.InlineKeyboardMarkup()
    first = types.InlineKeyboardButton('1', callback_data='answer_1')
    second = types.InlineKeyboardButton('2', callback_data='answer_2')
    third = types.InlineKeyboardButton('3', callback_data='answer_3')
    markup.row(first, second, third)
    next_quest = types.InlineKeyboardButton('Следующий вопрос', callback_data='next2_quest')
    markup.row(next_quest)
    main_menu_but = types.InlineKeyboardButton('Главное меню', callback_data='back_to_main')
    back_but = types.InlineKeyboardButton('К выбору квиза', callback_data='back_quiz_callback')
    markup.row(main_menu_but, back_but)
    while a > 0:
        if a == 1:
            bot.edit_message_text(chat_id=callback.message.chat.id, message_id=callback.message.id,
                              text=f'<b>Вы выбрали Квиз №{n} (Вопрос {a})</b> \n \n<b>Какой роман Федора Достоевского рассказывает историю бывшего студента, совершившего убийство?</b> \n \n1) "Преступление и наказание" 2) "Идиот" 3) "Братья Карамазовы"',
                              reply_markup=markup, parse_mode='html')
            correct_answer = 1
        elif a == 2:
            bot.edit_message_text(chat_id=callback.message.chat.id, message_id=callback.message.id,
                              text=f'<b>Вы выбрали Квиз №{n} (Вопрос {a})</b> \n \n<b>Кто написал повесть "Мертвые души"?</b> \n \n1) Иван Тургенев 2) Николай Гоголь 3) Михаил Лермонтов',
                              reply_markup=markup, parse_mode='html')
            correct_answer = 2
        elif a == 3:
            bot.edit_message_text(chat_id=callback.message.chat.id, message_id=callback.message.id,
                              text=f'<b>Вы выбрали Квиз №{n} (Вопрос {a})</b> \n \n<b>Как зовут героиню романа Александра Пушкина "Евгений Онегин"?</b> \n \n1) Татьяна Ларина 2) Ольга Ильинская 3) Мария Волконская',
                              reply_markup=markup, parse_mode='html')
            correct_answer = 1
        else:
            result_quest(callback)


""" Кнопка 'Назад' """

@bot.callback_query_handler(func=lambda call: call.data == 'back_quiz_callback')
def recomend_back_callback(callback):
    global a, score
    score = 0
    a = 1
    markup = types.InlineKeyboardMarkup()
    quiz_but1 = types.InlineKeyboardButton('Квиз 1', callback_data='quiz1_callback')
    quiz_but2 = types.InlineKeyboardButton('Квиз 2', callback_data='quiz2_callback')
    main_menu_but = types.InlineKeyboardButton('Главное меню', callback_data='back_to_main')
    markup.row(quiz_but1, quiz_but2)
    markup.row(main_menu_but)
    bot.edit_message_text(chat_id=callback.message.chat.id, message_id=callback.message.id, text='<b>Вы выбрали Квиз</b> \n \nВыберите квиз:', reply_markup=markup, parse_mode='html')


""" Выводит итоговый результат """

@bot.callback_query_handler(func=lambda call: call.data == 'result')
def result_quest(callback):
    global score, a
    markup = types.InlineKeyboardMarkup()
    main_menu_but = types.InlineKeyboardButton('Главное меню', callback_data='back_to_main')
    back_but = types.InlineKeyboardButton('К выбору квиза', callback_data='back_quiz_callback')
    markup.row(main_menu_but, back_but)
    bot.edit_message_text(chat_id=callback.message.chat.id, message_id=callback.message.id, text=f'<b>Вы выбрали Квиз №{n}</b>\n \nКвиз завершён, вот ваш результат: {score}', reply_markup=markup, parse_mode='html')


# Раздел Интересные факты

@bot.callback_query_handler(func=lambda call: call.data == 'fact_callback')
def fact_button_callback(callback):
    markup = types.InlineKeyboardMarkup()
    fact = types.InlineKeyboardButton('Интересный факт', callback_data='fact_but_callback')
    markup.row(fact)
    main_menu_but = types.InlineKeyboardButton('Главное меню', callback_data='back_to_main')
    markup.row(main_menu_but)
    bot.edit_message_text(chat_id=callback.message.chat.id, message_id=callback.message.id, text='<b>Вы выбрали Интересные факты</b>\n \nНачните поиск интересного факта:', reply_markup=markup, parse_mode='html')


@bot.callback_query_handler(func=lambda call: call.data == 'fact_but_callback')
def fact_button(callback):
    global facts
    markup = types.InlineKeyboardMarkup()
    next_fact = types.InlineKeyboardButton('Посмотреть ещё один факт', callback_data='next_but_fact')
    markup.row(next_fact)
    main_menu_but = types.InlineKeyboardButton('Главное меню', callback_data='back_to_main')
    markup.row(main_menu_but)
    bot.edit_message_text(chat_id=callback.message.chat.id, message_id=callback.message.id, text=f'<b>Вы выбрали Интересные факты</b>\n \nВот ваш интересный факт:\n \n{random.choice(facts)}', reply_markup=markup, parse_mode='html')


    """ Тут всякое разное """

@bot.callback_query_handler(func=lambda call: True)
def callback(call):
    global user_answer, correct_answer, a, score, liston
    if call.data == 'answer_1':  # Устанавливает ответ от пользоваителя 1
        user_answer = 1

    elif call.data == 'answer_2':  # Устанавливает ответ от пользоваителя 2
        user_answer = 2

    elif call.data == 'answer_3':  # Устанавливает ответ от пользоваителя 3
        user_answer = 3

    elif call.data == 'next1_quest':  # Обработчик кнопки 'Следующий вопрос'
        if user_answer == correct_answer:
            score += 1
            a += 1
            quiz1_callback(call)
        else:
            a += 1
            quiz1_callback(call)

    elif call.data == 'next2_quest':  # Обработчик кнопки 'Следующий вопрос'
        if user_answer == correct_answer:
            score += 1
            a += 1
            quiz2_callback(call)
        else:
            a += 1
            quiz2_callback(call)

    elif call.data == 'next_but_fact':
        fact_button(call)


bot.polling(none_stop=True)
