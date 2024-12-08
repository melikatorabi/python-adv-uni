import urllib.request
import json
import statistics

class StudentFetcher:
    def init(self):
        url = "https://cdn.ituring.ir/ex/users.json"
        try:
            with urllib.request.urlopen(url) as response:
                raw_data = response.read()
                self.students_data = json.loads(raw_data)
        except Exception as error:
            raise Exception(f"Error fetching data: {error}")

    def high_achievers(self):
        return {
            f"{student.get('first_name', 'N/A')} {student['last_name']}"
            for student in self.__students_data
            if student.get('score', 0) > 18.5
        }

    def top_performers(self):
        max_score = max(student.get('score', 0) for student in self.__students_data)
        return tuple(
            f"{student.get('first_name', 'N/A')} {student['last_name']}"
            for student in self.__students_data
            if student.get('score', 0) == max_score
        )

    def average_score(self):
        scores = [student.get('score', 0) for student in self.__students_data]
        return statistics.mean(scores)

    def filtered_students(self):
        return [
            {
                key: value
                for key, value in student.items()
                if key not in {'city', 'province', 'location'}
            }
            for student in self.__students_data
        ]

if __name == "main":
    student_fetcher = StudentFetcher()

    print("High achievers with scores above 18.5:")
    print(student_fetcher.high_achievers())

    print("\nTop performers with the highest score:")
    print(student_fetcher.top_performers())

    print("\nAverage score of all students:")
    print(student_fetcher.average_score())

    print("\nFiltered students list (without city, province, location):")
    print(student_fetcher.filtered_students())