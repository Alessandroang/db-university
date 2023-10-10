1. **Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia**

SELECT \*
FROM `students`
JOIN `degrees`
ON `degrees`.`name` = 'Corso di Laurea in Economia';

2. **Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze**

SELECT \*
FROM `degrees`
JOIN `departments`
ON `departments`.`name` = 'Dipartimento di Neuroscienze'
WHERE `level` = 'magistrale';

3. **Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)**

SELECT \*
FROM `courses`
JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
WHERE `course_teacher`.`teacher_id` = 44;

4. **Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome**

SELECT `students`.`name`, `students`.`surname`, `degrees`.`name`, `degrees`.`level`, `degrees`.`address`, `departments`.`name`
FROM `students`
JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`
JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`name` ASC , `students`.`surname`ASC ;

5. **Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti**

SELECT `degrees`.`name`, `courses`.`name`,`teachers`.`name`
FROM`degrees`
JOIN `courses`
ON `degrees`.`id` = `courses`.`degree_id`
JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers`
ON `course_teacher`.`teacher_id` = `teachers`.`id`;

6. **Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)**

SELECT `teachers`.`name`, `teachers`.`surname`, `departments`.`name`
FROM `teachers`
JOIN `course_teacher`
ON `teachers`.`id` = `course_teacher`.`teacher_id`
JOIN `courses`
ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `degrees`
ON `degrees`.`id` = `courses`.`degree_id`
JOIN `departments`
ON `departments`.`id` = `degrees`.`department_id`
WHERE `departments`.`name` = 'Dipartimento di Matematica';

7. **BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo.Successivamente, filtrare i tentativi con voto minimo 18.**

SELECT
COUNT(\*) AS `numero_tentativi`, `students`.`id` AS `id_studente`, `courses`.`id` AS `id_corso`, `courses`.`name` AS `nome_corso`
FROM `students`
JOIN `exam_student`
ON `students`.`id` = `exam_student`.`student_id`
JOIN `exams`
ON `exam_student`.`exam_id` = `exams`.`id`
JOIN `courses`
ON `exams`.`course_id` = `courses`.`id`
GROUP BY `students`.`id`, `courses`.`id`;
