### БАГ-РЕПОРТ #4 (детально)
**Название:** Валидация уникальности имени проекта отсутствует, сервер возвращает 500

**Приоритет:** High
**Серьезность:** Critical

**URL:** POST /push-console/api/v1/projects

**Передаваемые данные:**
{
    "name": "Тестовый проект 001"
}

**Ожидаемое поведение (согласно требованиям UC.KPS.A.05 EX1):**
- Статус код: 409 Conflict
- msg_code: "push_console_project_duplicate_name"
- Сообщение: "Project name already exists"

**Фактическое поведение:**
- Статус код: 500 Internal Server Error
- Тело: {"status":"ERROR","msg_code":"general_internal","data":null}

**Логи:**
```
2026-04-08 14:07:26.383488342
{"level":"error","ts":"2026-04-08T11:07:25.380720394Z","msg":"error with creating project name: test course error example","maturity":"5","req-id":"n/a","service_name":"kc_test_course ","caller":"/src/internal/service/project/project.go:83","trace-id":"n/a","app-id":"n/a"}
_msg	{"level":"error","ts":"2026-04-08T11:07:25.380720394Z","msg":"error with creating project name: test course error example","maturity":"5","req-id":"n/a","service_name":"kc_test_course ","caller":"/src/internal/service/project/project.go:83","trace-id":"n/a","app-id":"n/a"}
_stream	{}
_stream_id	0000000000000000e934a84adb05276890d7f7bfcadabe92
_time	2026-04-08T11:07:26.383488342Z
container_created_at	2026-03-31T08:00:04.229156667Z
container_id	d7394ac07133f4292a998178708d1a79e9bcc21f2ecb72b1da6d27e68a744a09
container_name	service-kc-tests-back-1-1
host	6890df11fdb3
image	push_back:1.0.0
label.com.docker.compose.config-hash	de13e8b1daf5706a58b034c7c97b1f282f0111ba3b08c447b7e386239a070ecb
label.com.docker.compose.container-number	1
label.com.docker.compose.image	sha256:9a070e070641df5e2e13381f20255558c885f6886ebf2571c6cfe64096195f19
label.com.docker.compose.oneoff	False
label.com.docker.compose.project	service
label.com.docker.compose.project.config_files	/home/teacher/teacher-test-course/service/docker-compose.yaml
label.com.docker.compose.project.working_dir	/home/teacher/teacher-test-course/service
label.com.docker.compose.service	kc-tests-back-1
label.com.docker.compose.version	5.0.2
message	{"level":"error","ts":"2026-04-08T11:07:25.380720394Z","msg":"error with creating project name: test course error example","maturity":"5","req-id":"n/a","service_name":"kc_test_course ","caller":"/src/internal/service/project/project.go:83","trace-id":"n/a","app-id":"n/a"}
source_type	docker_logs
stream	stderr
timestamp	2026-04-08T11:07:25.380825714Z
```

### БАГ-РЕПОРТ #5
**Название:** PUT /projects возвращает 500 при попытке использовать дубликат имени

**Приоритет:** High
**Серьезность:** Critical

**Метод:** PUT
**URL:** /push-console/api/v1/projects/{projectId}

**Передаваемые данные:**
```json
{
    "name": "Существующее_имя_проекта"
}
```

Ожидаемое поведение (согласно требованиям UC.KPS.A.17 EX2):

Статус код: 409 Conflict

msg_code: "push_console_project_duplicate_name"

Сообщение: "Project name already exists"

Фактическое поведение:

Статус код: 500 Internal Server Error

Тело ответа:

json
{
    "status": "ERROR",
    "msg_code": "general_internal",
    "data": null
}


**Логи:** 
```
http://193.169.128.91:9428/select/vmui/?#/?query=project&g0.range_input=5m&g0.end_input=2026-04-08T11%3A23%3A10&g0.relative_time=last_5_minutes&view=group

2026-04-08 14:22:06.270913191
{"level":"error","ts":"2026-04-08T11:22:05.268942317Z","msg":"error with updating project: test course error example","maturity":"5","req-id":"n/a","service_name":"kc_test_course ","caller":"/src/internal/service/project/project.go:237","trace-id":"n/a","app-id":"n/a"}
_msg	{"level":"error","ts":"2026-04-08T11:22:05.268942317Z","msg":"error with updating project: test course error example","maturity":"5","req-id":"n/a","service_name":"kc_test_course ","caller":"/src/internal/service/project/project.go:237","trace-id":"n/a","app-id":"n/a"}
_stream	{}
_stream_id	0000000000000000e934a84adb05276890d7f7bfcadabe92
_time	2026-04-08T11:22:06.270913191Z
container_created_at	2026-03-31T08:00:04.229156667Z
container_id	d7394ac07133f4292a998178708d1a79e9bcc21f2ecb72b1da6d27e68a744a09
container_name	service-kc-tests-back-1-1
host	6890df11fdb3
image	push_back:1.0.0
label.com.docker.compose.config-hash	de13e8b1daf5706a58b034c7c97b1f282f0111ba3b08c447b7e386239a070ecb
label.com.docker.compose.container-number	1
label.com.docker.compose.image	sha256:9a070e070641df5e2e13381f20255558c885f6886ebf2571c6cfe64096195f19
label.com.docker.compose.oneoff	False
label.com.docker.compose.project	service
label.com.docker.compose.project.config_files	/home/teacher/teacher-test-course/service/docker-compose.yaml
label.com.docker.compose.project.working_dir	/home/teacher/teacher-test-course/service
label.com.docker.compose.service	kc-tests-back-1
label.com.docker.compose.version	5.0.2
message	{"level":"error","ts":"2026-04-08T11:22:05.268942317Z","msg":"error with updating project: test course error example","maturity":"5","req-id":"n/a","service_name":"kc_test_course ","caller":"/src/internal/service/project/project.go:237","trace-id":"n/a","app-id":"n/a"}
source_type	docker_logs
stream	stderr
timestamp	2026-04-08T11:22:05.269113777Z
```

Вывод:
В коде используется заглушка "test course error example" вместо реальной проверки уникальности имени проекта. Проблема присутствует как в POST (создание), так и в PUT (обновление).



### БАГ-РЕПОРТ #6
### БАГ-РЕПОРТ #6
**Название:** DELETE /service-tokens возвращает 200 при удалении несуществующего токена

**Приоритет:** Medium
**Серьезность:** Major

**Метод:** DELETE
**URL:** /push-console/api/v1/projects/{projectId}/service-tokens/{invalidToken}

**Предусловие:**
- Существует проект с ID: 2779ab45-0d81-4fed-a606-c6bed7428673
- Токен "invalid-token-value-12345" не существует в системе

**Шаги воспроизведения:**
1. Отправить DELETE запрос на удаление несуществующего токена

**Фактический результат:**
- Статус код: 200 OK
- Тело ответа: {"status": "OK", "msg_code": "push_console_service_token_deleted"}

**Ожидаемый результат:**
- Статус код: 404 Not Found
- msg_code: "test_course_service_token_not_found"

**Нарушенный принцип REST:**
DELETE несуществующего ресурса должен возвращать 404 Not Found



### БАГ-РЕПОРТ #7
**Название:** GET /projects/{id} возвращает 500 при неверном формате UUID

**Приоритет:** Medium
**Серьезность:** Major

**Метод:** GET
**URL:** /push-console/api/v1/projects/12345

**Передаваемые данные:**
- id: "12345" (не UUID формат)

**Ожидаемое поведение (согласно Swagger):**
- Статус код: 400 Bad Request
- msg_code: "general_bad_request_error"

**Фактическое поведение:**
- Статус код: 500 Internal Server Error
- Тело ответа:
```json
{
    "status": "ERROR",
    "msg_code": "general_internal",
    "data": {
        "reason": "error with parsing project ID: invalid UUID length: 5"
    }
}

url для воспроизведения:

bash
curl -X GET "http://193.169.128.91/push-console/api/v1/projects/12345" \
  -H "Authorization: Bearer <token>"
```


### БАГ-РЕПОРТ №8
**Название:** DELETE /service-tokens возвращает 200, но токен не удаляется из БД/фронта

**Приоритет:** High
**Серьезность:** Critical

**Метод:** DELETE
**URL:** /push-console/api/v1/projects/{projectId}/service-tokens/{value}

**Передаваемые данные:**
- projectId: 7e2056e8-b6d3-4694-8e75-eb1f747a9c16
- value: QnaJn5sH6wkFsR69OLBBQxdrtCD4ZRRM+PfGtn...6dDpbStnf+QX6K+rilpqdWIQZ1Q+mEc2jGzt4l

**Шаги воспроизведения:**
1. Отправить DELETE запрос на удаление существующего сервисного токена
2. Получить ответ 200 OK с msg_code "push_console_service_token_deleted"
3. Проверить фронтенд или БД

**Ожидаемое поведение:**
- Токен должен быть удален из системы
- На фронтенде количество токенов должно уменьшиться

**Фактическое поведение:**
- API возвращает 200 OK (успешное удаление)
- На фронтенде токен остается в списке
- Количество токенов не изменилось (было 2, осталось 2)

**Доказательства:**
- Ответ API: 200 OK, "push_console_service_token_deleted"
- Фронтенд: токен все еще отображается в списке
- Количество токенов: "Создано 2 из 5 токенов" (не изменилось)

**curl для воспроизведения:**
```bash
curl -X DELETE "http://193.169.128.91/push-console/api/v1/projects/7e2056e8-b6d3-4694-8e75-eb1f747a9c16/service-tokens/QnaJn5sH6wkFsR69OLBBQxdrtCD4ZRRM+PfGtn...6dDpbStnf+QX6K+rilpqdWIQZ1Q+mEc2jGzt4l" \
  -H "Authorization: Bearer <token>"
```
