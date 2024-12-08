
class Student:
    def __init__(self, name, surname, gender):
        self.name = name
        self.surname = surname
        self.gender = gender
        self.finished_courses = []
        self.courses_in_progress = []
        self.grades = {}

    def rate_lec(self, lecturer, course, grade):
        if isinstance(lecturer, Lecturer) and (course in self.finished_courses or course in self.courses_in_progress) and course in lecturer.courses_attached:
            if course in lecturer.grades:
                lecturer.grades[course] += [grade]
            else:
                lecturer.grades[course] = [grade]
        else:
            return 'Ошибка'

    def __str__(self):
        all_grades = []
        for grades in self.grades.values():
            all_grades.extend(grades)
        return f"""Имя: {self.name}
Фамилия: {self.surname}
Средняя оценка за домашние задания: {sum(all_grades)/len(all_grades)}
Курсы в процессе изучения: {', '.join(self.courses_in_progress)}
Завершенные курсы: {', '.join(self.finished_courses)}"""

    def __eq__(self, other):
        if not isinstance(other, Student):
            return 'Ошибка'
        all_grades = []
        for grades in self.grades.values():
            all_grades.extend(grades)
        all_grades_other = []
        for grades in other.grades.values():
            all_grades_other.extend(grades)
        return sum(all_grades)/len(all_grades) == sum(all_grades_other)/len(all_grades_other)

    def __lt__(self, other):
        if not isinstance(other, Student):
            return 'Ошибка'
        all_grades = []
        for grades in self.grades.values():
            all_grades.extend(grades)
        all_grades_other = []
        for grades in other.grades.values():
            all_grades_other.extend(grades)
        return sum(all_grades)/len(all_grades) < sum(all_grades_other)/len(all_grades_other)

    def __le__(self, other):
        if not isinstance(other, Student):
            return 'Ошибка'
        all_grades = []
        for grades in self.grades.values():
            all_grades.extend(grades)
        all_grades_other = []
        for grades in other.grades.values():
            all_grades_other.extend(grades)
        return sum(all_grades)/len(all_grades) <= sum(all_grades_other)/len(all_grades_other)

class Mentor:
    def __init__(self, name, surname):
        self.name = name
        self.surname = surname
        self.courses_attached = []

class Lecturer(Mentor):
    def __init__(self, name, surname):
        super().__init__(name, surname)
        self.grades = {}

    def __str__(self):
        all_grades = []
        for grades in self.grades.values():
            all_grades.extend(grades)
        return f"""Имя: {self.name}
Фамилия: {self.surname}
Средняя оценка за лекции: {sum(all_grades)/len(all_grades)}"""

    def __eq__(self, other):
        if not isinstance(other, Lecturer):
            return 'Ошибка'
        all_grades = []
        for grades in self.grades.values():
            all_grades.extend(grades)
        all_grades_other = []
        for grades in other.grades.values():
            all_grades_other.extend(grades)
        return sum(all_grades)/len(all_grades) == sum(all_grades_other)/len(all_grades_other)

    def __lt__(self, other):
        if not isinstance(other, Lecturer):
            return 'Ошибка'
        all_grades = []
        for grades in self.grades.values():
            all_grades.extend(grades)
        all_grades_other = []
        for grades in other.grades.values():
            all_grades_other.extend(grades)
        return sum(all_grades)/len(all_grades) < sum(all_grades_other)/len(all_grades_other)

    def __le__(self, other):
        if not isinstance(other, Lecturer):
            return 'Ошибка'
        all_grades = []
        for grades in self.grades.values():
            all_grades.extend(grades)
        all_grades_other = []
        for grades in other.grades.values():
            all_grades_other.extend(grades)
        return sum(all_grades)/len(all_grades) <= sum(all_grades_other)/len(all_grades_other)

class Reviewer(Mentor):
    def rate_hw(self, student, course, grade):
        if isinstance(student, Student) and course in self.courses_attached and course in student.courses_in_progress:
            if course in student.grades:
                student.grades[course] += [grade]
            else:
                student.grades[course] = [grade]
        else:
            return 'Ошибка'

    def __str__(self):
        return f"""Имя: {self.name}
        Фамилия: {self.surname}"""

def average_grade_for_course(students, course):
    all_grades = []
    for student in students:
        if course in student.grades:
            all_grades.extend(student.grades[course])
    return sum(all_grades)/len(all_grades)

def average_grade_for_course_lecturers(lecturers, course):
    all_grades = []
    for lecturer in lecturers:
        if course in lecturer.grades:
            all_grades.extend(lecturer.grades[course])
    return sum(all_grades)/len(all_grades)

best_student = Student('Ruoy', 'Eman', 'your_gender')
best_student.courses_in_progress += ['Python']
best_student.grades = {'Python': [10, 9, 10, 7, 8]}

best_student1 = Student('Ruoy', 'Eman', 'your_gender')
best_student1.courses_in_progress += ['Python']
best_student1.grades = {'Python': [10, 9, 10, 7, 8]}

cool_mentor = Lecturer('Some', 'Buddy')
cool_mentor.courses_attached += ['Python']

best_student.rate_lec(cool_mentor, "Python", 9)
best_student.rate_lec(cool_mentor, "Python", 8)

cool_mentor1 = Lecturer('Some', 'Buddy')
cool_mentor1.courses_attached += ['Python']

best_student.rate_lec(cool_mentor1, "Python", 7)
best_student.rate_lec(cool_mentor1, "Python", 6)

lecturers = [cool_mentor, cool_mentor1]
print(average_grade_for_course_lecturers(lecturers, "Python"))

print(cool_mentor.grades)
print(cool_mentor)
print(best_student)
print(cool_mentor == cool_mentor1)
print(cool_mentor < cool_mentor1)
print(cool_mentor >= cool_mentor1)
print(best_student == best_student1)
print(best_student < best_student1)
print(best_student >= best_student1)

