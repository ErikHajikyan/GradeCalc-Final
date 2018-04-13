import json


def loadgradebreakdown():
    with open ('gc_setup.json') as data_file:
        course = json.load(data_file)
    grade_breakdown = course['course_setup']['grade_breakdown']
    return grade_breakdown


def loadgc_grades():
    try:
        with open('gc_grades.json') as data_file1:
            gc_grades = json.load(data_file1)
        return gc_grades
    except:
        the_file = open('gc_grades.json', 'w')
        the_file.write('{}')
        the_file.close()
        with open('gc_grades.json') as data_file1:
            gc_grades = json.load(data_file1)
        return gc_grades


def askforinfo():
    print("Enter your name here: ")
    name = str(raw_input())
    return name


def change_grades(gc_grades, name, grade_breakdown):
    if name in gc_grades:
        for key in gc_grades[name]:
            print"Your grade for " + key + 'is ' + str(gc_grades[name][key])
            x = str(raw_input('Do you want to change your grade?(Input Yes or No)'))
            if x == str('Yes'):
                gc_grades[name][key] = acceptableGrade(key)
        return gc_grades
    else:
        current_grades = {name: {}}
        for key in grade_breakdown:
            print('The grade for ' + key + " is" + str(grade_breakdown[key])) + "%"
            current_grades[name][key] = acceptableGrade(key)
        return current_grades

def acceptableGrade(key):
    x = input("What is your Current Grade for " + key + " Please insert -1 if you don't have a grade yet")
    if x <= 100 and x >= -1:
        return x
    else:
        print "The number is out of the acceptable range!"
        x = acceptableGrade(key)
        return x

def saveGrades(gc_grades, new_grades, userinfo):
    gc_grades[userinfo] = new_grades[userinfo]
    file = open("gc_grades.json", "w")
    file.write(json.dumps(gc_grades))
    file.close()


def printcurrentgrade(grades, current_grades, name):
    curr_grade = 0
    for key in current_grades[name]:
        if current_grades[name][key] != -1:
            try:
                calc_grade = float(current_grades[name][key]) * grades[key] / 100
                curr_grade = curr_grade + calc_grade
            except:
                print "Not a number input"
    return curr_grade


def loadconv_matrix():
    with open ('gc_setup.json') as data_file2:
        gc_setup = json.load(data_file2)
        conv_matrix = gc_setup['course_setup']['conv_matrix']
    return conv_matrix

def printCurrentLetter(curr_grade, conv_matrix):
    for z in range(len(conv_matrix)):
        if int(curr_grade) >= conv_matrix[z]["min"]:
            print "Your final  grade is " + str(curr_grade) + " Your final letter grade is " + str(conv_matrix[z]["mark"])
            break


def main():
    name = askforinfo()
    grade_breakdown = loadgradebreakdown()
    gc_grades = loadgc_grades()
    new_grades = change_grades(gc_grades, name, grade_breakdown)
    saveGrades(gc_grades, new_grades, name)
    curr_grade = printcurrentgrade(grade_breakdown, new_grades, name)
    conv_matrix = loadconv_matrix()
    printCurrentLetter(curr_grade, conv_matrix)


main()
