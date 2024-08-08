<div class="lesson-question"><div class="lesson-description"><h3 class="step-content-head"><strong>Условие:</strong></h3>

<p>&nbsp;</p>

<p>Склонируйте проект по <a href="https://github.com/KataAcademy/PP_3_1_2_Boot_Security" target="_blank">ссылке</a>&nbsp;и просмотрите его.</p>

<div class="lesson-question">
<div class="lesson-description">
<p>Модуль Spring Security позволяет нам внедрять права доступа, а также контролировать их исполнение без ручных проверок.<br>
Spring Security базируется на 2х интерфейсах, которые определяют связь сущностей с секьюрностью:&nbsp;<code>UserDetails&nbsp;</code>и&nbsp;<code>GrantedAuthority</code>.<br>
<code>UserDetails&nbsp;</code>— то, что будет интерпретироваться системой как пользователь.<br>
<code>GrantedAuthority&nbsp;</code>— сущность, описывающая права юзера.<br>
Оба эти интерфейса имеют множество реализаций: просмотрите класс WebSecurityConfig, в методе&nbsp;<code>configure()</code> с помощью настроек userDetailsService<code>()</code>&nbsp;мы собираем единственный на всю программу экземпляр&nbsp;<code>UserDetails&nbsp;</code>с именем и паролем user , а его роль “USER” так же будет преобразована в экземпляр <code>GrantedAuthority</code>.</p>

<p>Это простейший способ создания секьюрности. Так же мы можем использовать jdbc-аутентификацию путем написания запроса, возвращающего пользователя и роль.<br>
Как вы понимаете, такие способы максимально просты, но лишены достаточной гибкости, потому наиболее часто используемый вариант настройки выглядит как имплементация&nbsp;<code>UserDetails&nbsp;</code>и&nbsp;<code>GrantedAuthority&nbsp;</code>в классах-сущностях с переопределением существующих методов.</p>

<p>Рассмотрим приложение.<br>
Новые классы:<br>
- <code>WebSecurityConfig&nbsp;</code>— настройка секьюрности по определенным URL, а также настройка&nbsp;<code>UserDetails&nbsp;</code>и&nbsp;<code>GrantedAuthority</code>.<br>
-&nbsp;<code>LoginSuccessHandler&nbsp;</code>— хэндлер, содержащий в себе алгоритм действий при успешной аутентификации. Например, тут мы можем отправить пользователя с ролью админа на админку после логина, а с ролью юзер на главную страницу сайта и т.п.&nbsp;</p>

<p>&nbsp;</p>

<h3><strong>Задание:&nbsp;</strong></h3>

<p><br>
1. Перенесите классы и зависимости из предыдущей задачи.<br>
2. Создайте класс&nbsp;<code>Role&nbsp;</code>и свяжите&nbsp;<code>User&nbsp;</code>с ролями так, чтобы юзер мог иметь несколько ролей.<br>
3. Имплементируйте модели&nbsp;<code>Role&nbsp;</code>и&nbsp;<code>User&nbsp;</code>интерфейсами&nbsp;<code>GrantedAuthority и&nbsp;UserDetails</code><code>&nbsp;</code>соответственно. Измените настройку секьюрности с&nbsp;<code>inMemory&nbsp;</code>на&nbsp;<code>userDetailService</code>.<br>
4. Все CRUD-операции и страницы для них должны быть доступны только пользователю с ролью&nbsp;<code>admin&nbsp;</code>по url:&nbsp;<code>/admin/</code>.<br>
5. Пользователь с ролью&nbsp;<code>user&nbsp;</code>должен иметь доступ только к своей домашней странице&nbsp;<code>/user</code>, где выводятся его данные. Доступ к этой странице должен быть только у пользователей с ролью&nbsp;<code>user </code>и&nbsp;<code>admin</code>. Не забывайте про несколько ролей у пользователя!<br>
6. Настройте&nbsp;<code>logout&nbsp;</code>с любой страницы с использованием возможностей thymeleaf.<br>
7. Настройте&nbsp;<code>LoginSuccessHandler&nbsp;</code>так, чтобы админа после аутентификации направляло на страницу<code>&nbsp;/admin</code>, а юзера на его страницу /user.</p>
</div>