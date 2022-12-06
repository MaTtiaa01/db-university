Group by:
  1  Contare quanti iscritti ci sono stati ogni anno
  2  Contare gli insegnanti che hanno l'ufficio nello stesso edificio
  3  Calcolare la media dei voti di ogni appello d'esame
  4  Contare quanti corsi di laurea ci sono per ogni dipartimento
Join:
   5  Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
   6  Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
   7  Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
   8  Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
   9  Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
   10  Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per superare ciascuno dei suoi esami

```sql
 1# SELECT COUNT(`students`.`id`) AS `students_number`, YEAR(`students`.`enrolment_date`) AS `year` FROM `students` GROUP BY  `year`; 
 
 2# SELECT COUNT(`id`) , `office_address` FROM `teachers` GROUP BY `office_address`;
 
 3# SELECT AVG(`exam_student`.`vote`), `exam_student`.`exam_id` FROM `exam_student` GROUP BY `exam_student`.`exam_id`;
 
 4# SELECT `degrees`.`department_id` AS `department_id`, COUNT(`degrees`.`name`) AS `degree_number` 
    FROM `degrees`
    GROUP BY `department_id`;
 
 5# SELECT `students`.`name`,`students`.`id`,`students`.`surname`,`students`.`registration_number`,        `degrees`.`name` AS `deegre_name`
      FROM `degrees`
      JOIN `students`
      ON `students`.`degree_id` = `degrees`.`id`
      WHERE `degrees`.`name` = "Corso di Laurea in Economia";
 
 6# SELECT `degrees`.`level`, `degrees`.`name` AS `degree_name`, `departments`.`name`
    FROM `departments`
    JOIN `degrees`
    ON `degrees`.`department_id` = `departments`.`id`
    WHERE `departments`.`name` = "Dipartimento di Neuroscienze";
 
 7# SELECT `courses`.`name` AS `course_name` , `teachers`.`id`, `teachers`.`name`, `teachers`.`surname`
      FROM `courses`
      JOIN `course_teacher`
      ON `course_teacher`.`course_id` = `courses`.`id`
      JOIN `teachers`
      ON `course_teacher`.`teacher_id` = `teachers`.`id`
      WHERE `teachers`.`id` = 44;
  
  8# SELECT `students`.`name` AS `student_name`, `students`.`surname` AS `student_surname`,`students`.`registration_number` AS `student_registration_number`, `degrees`.`name` AS `degree_name`, `departments`.`name` AS `department_name`
      FROM `departments`
      JOIN `degrees`
      ON `degrees`.`department_id` = `departments`.`id`
      JOIN `students`
      ON `students`.`degree_id` = `degrees`.`id`
      ORDER BY `students`.`name`, `students`.`surname` ASC;

  9# SELECT `degrees`.`name` AS `degree_name`, `courses`.`name` AS `course_name`, `teachers`.`name` AS  `teachers_name`, `teachers`.`surname` AS `teachers_surname`
    FROM `degrees`
    JOIN `courses`
    ON `courses`.`degree_id` = `degrees`.`id`
    JOIN `course_teacher`
    ON `course_teacher`.`course_id` = `courses`.`id`
    JOIN `teachers`
    ON `course_teacher`.`teacher_id` = `teachers`.`id`;
  
  10# SELECT DISTINCT `teachers`.`name` AS `teacher_name`, `teachers`.`surname` AS `teacher_surname`, `teachers`.`id` AS `teacher_id`, `departments`.`name` AS `department_name`, `courses`.`name` AS `courses_name`
      FROM `departments`
      JOIN `degrees`
      ON `degrees`.`department_id` = `departments`.`id`
      JOIN `courses`
      ON `courses`.`degree_id` = `degrees`.`id`
      JOIN `course_teacher`
      ON `course_teacher`.`course_id` = `courses`.`id`
      JOIN `teachers`
      ON `course_teacher`.`teacher_id` = `teachers`.`id`
      WHERE `departments`.`name` = "Dipartimento di Matematica";
      
```