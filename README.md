# Страница дневника стажера
Функционал страницы зависит от роли пользователя. Смотри подробнее в разделе "Логика работы"

## Логическая карта

- ТУТ БУДЕТ КАРТИНКА КОТОРОЙ ЕЩЕ НЕТ

## Логика работы

- role = user
  - Если статус сотрудника != challenger developer
    - Проверить числятся ли стажеры под контролем пользователя
      - Поле mentorOfUsers у используеммого в данный момент пользователя пользователя
    - Если числятся
      - Загрузить список стажеров, которые относятся к пользователю
        - При клике на стажера - открывается дневник стажировки
          - Доступно только заполнение еженедельных отчетов
    - Если не числяться
      - Редирект на "У вас нет стажеров"/"У вас недостаточно прав"
- Если роль = admin
  - Зпгрузить весь список пользователей, статус которых = challenger developer и которые относятся к оффису базирования используемого в данный момент юзера
    - При клике на стажера - открывается его дневник стажировки
      - Доступно подтверждение выполнения заданий
- role = user & status = "challenger developer"
  - Найти и загрузить дневник стажировки по id пользователя
    - Есть возможность отмечать выполненные задания.

## Функционал

- Задания
  - user & "challenger developer"
    - отметка о выполнении задания
  - admin 
    - подтверждающая отметка о выполнении задания
- Недельные отчеты
  - user & mentorOfUsers
    - Заполнение еженедельного отчета о проделанной работе

## Формат данных
```json5
{
  users: [
    {
      id: 'userId',
      role: 'userRole',
      mentorOfUsers?: [
            'userId(1)'..'userId(n)'
      ],
    },
  ],
  office: [
    {
      id: 'officeId',
      departments?: [
        'departmentId(1)'..'departmentId(n)',
      ]
    }
  ],
  departments: [
    {
      id: 'departmentId',
      leadsId: 'userId'
    }
  ],
  diary: [
    {
      id: 'diaryId',
      userId: 'userId',
      mentorId: 'mentorId',
      adminId: 'adminId',
      events: [
        {
          id: 'eventId',
          startTime: 'date',
          eventname: 'some event name',
          status: boolean,
          approved: boolean,
        }
      ],
      chart: [
        {
          id: 'chartId',
          userId: 'userId'
          mentorId: 'mentorId',
          date: 'some date',
          text: [
            'task 1 done'..'task 4 done'
          ]
        }
      ]
    }
  ]
}
```