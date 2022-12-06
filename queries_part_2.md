<!-- GROUP BY: -->

1)Contare quanti iscritti ci sono stati ogni anno
```sql
SELECT YEAR(`enrolment_date`) AS `Year`, COUNT(`id`) AS `Enroled_Number`
FROM `students`
GROUP BY `Year`;
```

2)Contare gli insegnanti che hanno l'ufficio nello stesso edificio
```sql
SELECT `office_address`, COUNT(`id`) AS `Teachers_Number`
FROM `teachers`
GROUP BY `office_address`;
```

3)Calcolare la media dei voti di ogni appello d'esame
```sql
SELECT `exam_id`, AVG(`vote`) AS `Average_Vote`
FROM `exam_student`
GROUP BY `exam_id`;
```

4)Contare quanti corsi di laurea ci sono per ogni dipartimento
```sql
SELECT `department_id` AS `Department_Number`, COUNT(`id`) as `Degree_Courses`
FROM `degrees`
GROUP BY `department_id`;
```


<!-- JOIN: -->

1)Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
```sql
SELECT `students`.`name` AS `Student_Name`, `students`.`surname` AS `Student_Surname`, `degrees`.`name` AS `Degree_Name`
FROM `students`
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = "Corso di Laurea in Economia";
```

2)Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
```sql
SELECT `degrees`.`name` AS `Degree_Name`, `departments`.`name` AS `Department_Name`
FROM `degrees`
JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`
WHERE `departments`.`name` = "Dipartimento di Neuroscienze" AND `degrees`.`level` = "magistrale";
```

3)Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
```sql
SELECT `courses`.`name` AS `Course_Name` , `teachers`.`name` AS `Teacher_Name`, `teachers`.`surname` AS `Teacher_Surname`
FROM `course_teacher`
JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`
WHERE `teachers`.`id` = 44;
```

4)Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono
    iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
```sql
SELECT `degrees`.`*`, `students`.`name` AS `Student_Name`,`students`.`surname` AS `Student_Surname`, `departments`.`name` AS `Department_Name`
FROM `degrees`
JOIN `students` ON `degrees`.`id` = `students`.`degree_id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`surname` ASC, `students`.`name` ASC;
```

5)Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
```sql
SELECT `degrees`.`name` AS `Degree_Name`, `courses`.`name` AS `Course_Name`, `teachers`.`name` AS `Teacher_Name`, `teachers`.`surname` AS `Teacher_Surname`
FROM `course_teacher`
JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `degrees` ON `degrees`.`id` = `courses`.`degree_id`;
```

6)Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
```sql
SELECT DISTINCT `teachers`.`*`, `departments`.`name` AS `Department_Name`
FROM `course_teacher`
JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`
JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `degrees` ON `degrees`.`id` = `courses`.`degree_id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = "Dipartimento di Matematica";
```

BONUS)Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per superare ciascuno dei suoi esami
```sql
SELECT `students`.`name` AS `Student_Name`, `students`.`surname` AS `Student_Surname`, `exam_student`.`*`, `courses`.`id` AS `Course_ID`, `courses`.`name` AS `Course_Name`
FROM `exam_student`
JOIN `students` ON `exam_student`.`student_id` = `students`.`id`
JOIN `exams` ON `exam_student`.`exam_id` = `exams`.`id`
JOIN `courses` ON `exams`.`course_id` = `courses`.`id`
/* GROUP BY / WHERE COUNT() `exam_student`.`vote` >= 18 ?; */
```