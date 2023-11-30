# Projeto Banco de Dados NoSQL

Atividade 2 - Projeto
Usando a base de dados de exemplo do livro, escolha um dos bancos NoSQL visto em aula (wide-colum storage, document storage ou graph database) e escreva os scripts necessários para salvar os mesmos dados no formato do banco escolhido. Faça as modificações necessárias nas relações dos dados para armazenar da melhor forma possível no banco NoSQL escolhido.

Além do script para a escrita dos dados no banco, faça as mesmas queries da atividade 1 no banco que você escolheu (estas queries devem estar no repositório junto com o script).

A entrega deverá ser o endereço de um repositório público no Github, sendo que o projeto pode conter até 3 pessoas da sua turma de laboratório.



# Realização

Utilizamos o MongoDB para realização desse projeto. Criamos um db no MongoDB Atlas e o preenchemos com comandos pelo MongoDB shell.

# Comandos para criação da tabela:


// Deletar dados existentes
db.prereq.deleteMany({});
db.time_slot.deleteMany({});
db.advisor.deleteMany({});
db.takes.deleteMany({});
db.student.deleteMany({});
db.teaches.deleteMany({});
db.section.deleteMany({});
db.instructor.deleteMany({});
db.course.deleteMany({});
db.department.deleteMany({});
db.classroom.deleteMany({});

// Inserir dados nas coleções
db.classroom.insertMany([
  { building: 'Packard', room_number: '101', capacity: 500 },
  { building: 'Painter', room_number: '514', capacity: 10 },
  { building: 'Taylor', room_number: '3128', capacity: 70 },
  { building: 'Watson', room_number: '100', capacity: 30 },
  { building: 'Watson', room_number: '120', capacity: 50 }
]);

db.department.insertMany([
  { dept_name: 'Biology', building: 'Watson', budget: 90000 },
  { dept_name: 'Comp. Sci.', building: 'Taylor', budget: 100000 },
  { dept_name: 'Elec. Eng.', building: 'Taylor', budget: 85000 },
  { dept_name: 'Finance', building: 'Painter', budget: 120000 },
  { dept_name: 'History', building: 'Painter', budget: 50000 },
  { dept_name: 'Music', building: 'Packard', budget: 80000 },
  { dept_name: 'Physics', building: 'Watson', budget: 70000 }
]);

db.course.insertMany([
  { course_id: 'BIO-101', title: 'Intro. to Biology', dept_name: 'Biology', credits: 4 },
  { course_id: 'BIO-301', title: 'Genetics', dept_name: 'Biology', credits: 4 },
  { course_id: 'BIO-399', title: 'Computational Biology', dept_name: 'Biology', credits: 3 },
  { course_id: 'CS-101', title: 'Intro. to Computer Science', dept_name: 'Comp. Sci.', credits: 4 },
  { course_id: 'CS-190', title: 'Game Design', dept_name: 'Comp. Sci.', credits: 4 },
  { course_id: 'CS-315', title: 'Robotics', dept_name: 'Comp. Sci.', credits: 3 },
  { course_id: 'CS-319', title: 'Image Processing', dept_name: 'Comp. Sci.', credits: 3 },
  { course_id: 'CS-347', title: 'Database System Concepts', dept_name: 'Comp. Sci.', credits: 3 },
  { course_id: 'EE-181', title: 'Intro. to Digital Systems', dept_name: 'Elec. Eng.', credits: 3 },
  { course_id: 'FIN-201', title: 'Investment Banking', dept_name: 'Finance', credits: 3 },
  { course_id: 'HIS-351', title: 'World History', dept_name: 'History', credits: 3 },
  { course_id: 'MU-199', title: 'Music Video Production', dept_name: 'Music', credits: 3 },
  { course_id: 'PHY-101', title: 'Physical Principles', dept_name: 'Physics', credits: 4 }
]);

db.instructor.insertMany([
  { ID: '10101', name: 'Srinivasan', dept_name: 'Comp. Sci.', salary: 65000 },
  { ID: '12121', name: 'Wu', dept_name: 'Finance', salary: 90000 },
  { ID: '15151', name: 'Mozart', dept_name: 'Music', salary: 40000 },
  { ID: '22222', name: 'Einstein', dept_name: 'Physics', salary: 95000 },
  { ID: '32343', name: 'El Said', dept_name: 'History', salary: 60000 },
  { ID: '33456', name: 'Gold', dept_name: 'Physics', salary: 87000 },
  { ID: '45565', name: 'Katz', dept_name: 'Comp. Sci.', salary: 75000 },
  { ID: '58583', name: 'Califieri', dept_name: 'History', salary: 62000 },
  { ID: '76543', name: 'Singh', dept_name: 'Finance', salary: 80000 },
  { ID: '76766', name: 'Crick', dept_name: 'Biology', salary: 72000 },
  { ID: '83821', name: 'Brandt', dept_name: 'Comp. Sci.', salary: 92000 },
  { ID: '98345', name: 'Kim', dept_name: 'Elec. Eng.', salary: 80000 }
]);

db.section.insertMany([
  { course_id: 'BIO-101', sec_id: '1', semester: 'Summer', year: 2017, building: 'Painter', room_number: '514', time_slot_id: 'B' },
  { course_id: 'BIO-301', sec_id: '1', semester: 'Summer', year: 2018, building: 'Painter', room_number: '514', time_slot_id: 'A' },
  { course_id: 'CS-101', sec_id: '1', semester: 'Fall', year: 2017, building: 'Packard', room_number: '101', time_slot_id: 'H' },
  { course_id: 'CS-101', sec_id: '1', semester: 'Spring', year: 2018, building: 'Packard', room_number: '101', time_slot_id: 'F' },
  { course_id: 'CS-190', sec_id: '1', semester: 'Spring', year: 2017, building: 'Taylor', room_number: '3128', time_slot_id: 'E' },
  { course_id: 'CS-190', sec_id: '2', semester: 'Spring', year: 2017, building: 'Taylor', room_number: '3128', time_slot_id: 'A' },
  { course_id: 'CS-315', sec_id: '1', semester: 'Spring', year: 2018, building: 'Watson', room_number: '120', time_slot_id: 'D' },
  { course_id: 'CS-319', sec_id: '1', semester: 'Spring', year: 2018, building: 'Watson', room_number: '100', time_slot_id: 'B' },
  { course_id: 'CS-319', sec_id: '2', semester: 'Spring', year: 2018, building: 'Taylor', room_number: '3128', time_slot_id: 'C' },
  { course_id: 'CS-347', sec_id: '1', semester: 'Fall', year: 2017, building: 'Taylor', room_number: '3128', time_slot_id: 'A' },
  { course_id: 'EE-181', sec_id: '1', semester: 'Spring', year: 2017, building: 'Taylor', room_number: '3128', time_slot_id: 'C' },
  { course_id: 'FIN-201', sec_id: '1', semester: 'Spring', year: 2018, building: 'Packard', room_number: '101', time_slot_id: 'B' },
  { course_id: 'HIS-351', sec_id: '1', semester: 'Spring', year: 2018, building: 'Painter', room_number: '514', time_slot_id: 'C' },
  { course_id: 'MU-199', sec_id: '1', semester: 'Spring', year: 2018, building: 'Packard', room_number: '101', time_slot_id: 'D' },
  { course_id: 'PHY-101', sec_id: '1', semester: 'Fall', year: 2017, building: 'Watson', room_number: '100', time_slot_id: 'A' },
]);

db.takes.insertMany([
  { ID: '00128', course_id: 'CS-101', sec_id: '1', semester: 'Fall', year: 2017, grade: 'A' },
  { ID: '00128', course_id: 'CS-347', sec_id: '1', semester: 'Fall', year: 2017, grade: 'A-' },
  { ID: '12345', course_id: 'CS-101', sec_id: '1', semester: 'Fall', year: 2017, grade: 'C' },
  { ID: '12345', course_id: 'CS-190', sec_id: '2', semester: 'Spring', year: 2017, grade: 'A' },
  { ID: '12345', course_id: 'CS-315', sec_id: '1', semester: 'Spring', year: 2018, grade: 'A' },
  { ID: '12345', course_id: 'CS-347', sec_id: '1', semester: 'Fall', year: 2017, grade: 'A' },
  { ID: '19991', course_id: 'HIS-351', sec_id: '1', semester: 'Spring', year: 2018, grade: 'B' },
  { ID: '23121', course_id: 'FIN-201', sec_id: '1', semester: 'Spring', year: 2018, grade: 'C+' },
  { ID: '44553', course_id: 'PHY-101', sec_id: '1', semester: 'Fall', year: 2017, grade: 'B-' },
  { ID: '45678', course_id: 'CS-101', sec_id: '1', semester: 'Fall', year: 2017, grade: 'F' },
  { ID: '45678', course_id: 'CS-101', sec_id: '1', semester: 'Spring', year: 2018, grade: 'B+' },
  { ID: '45678', course_id: 'CS-319', sec_id: '1', semester: 'Spring', year: 2018, grade: 'B' },
  { ID: '54321', course_id: 'CS-101', sec_id: '1', semester: 'Fall', year: 2017, grade: 'A-' },
  { ID: '54321', course_id: 'CS-190', sec_id: '2', semester: 'Spring', year: 2017, grade: 'B+' },
  { ID: '55739', course_id: 'MU-199', sec_id: '1', semester: 'Spring', year: 2018, grade: 'A-' },
  { ID: '76543', course_id: 'CS-101', sec_id: '1', semester: 'Fall', year: 2017, grade: 'A' },
  { ID: '76543', course_id: 'CS-319', sec_id: '2', semester: 'Spring', year: 2018, grade: 'A' },
  { ID: '76653', course_id: 'EE-181', sec_id: '1', semester: 'Spring', year: 2017, grade: 'C' },
  { ID: '98765', course_id: 'CS-101', sec_id: '1', semester: 'Fall', year: 2017, grade: 'C-' },
  { ID: '98765', course_id: 'CS-315', sec_id: '1', semester: 'Spring', year: 2018, grade: 'B' },
  { ID: '98988', course_id: 'BIO-101', sec_id: '1', semester: 'Summer', year: 2017, grade: 'A' },
  { ID: '98988', course_id: 'BIO-301', sec_id: '1', semester: 'Summer', year: 2018, grade: null },
]);

db.time_slot.insertMany([
  { time_slot_id: 'A', day: 'M', start_hr: 8, start_min: 0, end_hr: 8, end_min: 50 },
  { time_slot_id: 'A', day: 'W', start_hr: 8, start_min: 0, end_hr: 8, end_min: 50 },
  { time_slot_id: 'A', day: 'F', start_hr: 8, start_min: 0, end_hr: 8, end_min: 50 },
  { time_slot_id: 'B', day: 'M', start_hr: 9, start_min: 0, end_hr: 9, end_min: 50 },
  { time_slot_id: 'B', day: 'W', start_hr: 9, start_min: 0, end_hr: 9, end_min: 50 },
  { time_slot_id: 'B', day: 'F', start_hr: 9, start_min: 0, end_hr: 9, end_min: 50 },
  { time_slot_id: 'C', day: 'M', start_hr: 11, start_min: 0, end_hr: 11, end_min: 50 },
  { time_slot_id: 'C', day: 'W', start_hr: 11, start_min: 0, end_hr: 11, end_min: 50 },
  { time_slot_id: 'C', day: 'F', start_hr: 11, start_min: 0, end_hr: 11, end_min: 50 },
  { time_slot_id: 'D', day: 'M', start_hr: 13, start_min: 0, end_hr: 13, end_min: 50 },
  { time_slot_id: 'D', day: 'W', start_hr: 13, start_min: 0, end_hr: 13, end_min: 50 },
  { time_slot_id: 'D', day: 'F', start_hr: 13, start_min: 0, end_hr: 13, end_min: 50 },
  { time_slot_id: 'E', day: 'T', start_hr: 10, start_min: 30, end_hr: 11, end_min: 45 },
  { time_slot_id: 'E', day: 'R', start_hr: 10, start_min: 30, end_hr: 11, end_min: 45 },
  { time_slot_id: 'F', day: 'T', start_hr: 14, start_min: 30, end_hr: 15, end_min: 45 },
  { time_slot_id: 'F', day: 'R', start_hr: 14, start_min: 30, end_hr: 15, end_min: 45 },
  { time_slot_id: 'G', day: 'M', start_hr: 16, start_min: 0, end_hr: 16, end_min: 50 },
  { time_slot_id: 'G', day: 'W', start_hr: 16, start_min: 0, end_hr: 16, end_min: 50 },
  { time_slot_id: 'G', day: 'F', start_hr: 16, start_min: 0, end_hr: 16, end_min: 50 },
  { time_slot_id: 'H', day: 'W', start_hr: 10, start_min: 0, end_hr: 12, end_min: 30 },
]);

db.prereq.insertMany([
  { course_id: 'BIO-301', prereq_id: 'BIO-101' },
  { course_id: 'BIO-399', prereq_id: 'BIO-101' },
  { course_id: 'CS-190', prereq_id: 'CS-101' },
  { course_id: 'CS-315', prereq_id: 'CS-101' },
  { course_id: 'CS-319', prereq_id: 'CS-101' },
  { course_id: 'CS-347', prereq_id: 'CS-101' },
  { course_id: 'EE-181', prereq_id: 'PHY-101' },
]);

db.teaches.insertMany([
  { instructor_id: '10101', course_id: 'CS-101', section_id: '1', semester: 'Fall', year: 2017 },
  { instructor_id: '10101', course_id: 'CS-315', section_id: '1', semester: 'Spring', year: 2018 },
  { instructor_id: '10101', course_id: 'CS-347', section_id: '1', semester: 'Fall', year: 2017 },
  { instructor_id: '12121', course_id: 'FIN-201', section_id: '1', semester: 'Spring', year: 2018 },
  { instructor_id: '15151', course_id: 'MU-199', section_id: '1', semester: 'Spring', year: 2018 },
  { instructor_id: '22222', course_id: 'PHY-101', section_id: '1', semester: 'Fall', year: 2017 },
  { instructor_id: '32343', course_id: 'HIS-351', section_id: '1', semester: 'Spring', year: 2018 },
  { instructor_id: '45565', course_id: 'CS-101', section_id: '1', semester: 'Spring', year: 2018 },
  { instructor_id: '45565', course_id: 'CS-319', section_id: '1', semester: 'Spring', year: 2018 },
  { instructor_id: '76766', course_id: 'BIO-101', section_id: '1', semester: 'Summer', year: 2017 },
  { instructor_id: '76766', course_id: 'BIO-301', section_id: '1', semester: 'Summer', year: 2018 },
  { instructor_id: '83821', course_id: 'CS-190', section_id: '1', semester: 'Spring', year: 2017 },
  { instructor_id: '83821', course_id: 'CS-190', section_id: '2', semester: 'Spring', year: 2017 },
  { instructor_id: '83821', course_id: 'CS-319', section_id: '2', semester: 'Spring', year: 2018 },
  { instructor_id: '98345', course_id: 'EE-181', section_id: '1', semester: 'Spring', year: 2017 },
]);

db.advisor.insertMany([
  { s_ID: '00128', i_ID: '45565' },
  { s_ID: '12345', i_ID: '10101' },
  { s_ID: '19991', i_ID: '76543' },
  { s_ID: '44553', i_ID: '22222' },
  { s_ID: '45678', i_ID: '22222' },
  { s_ID: '76543', i_ID: '45565' },
  { s_ID: '76653', i_ID: '98345' },
  { s_ID: '98765', i_ID: '98345' },
  { s_ID: '98988', i_ID: '76766' },
]);

db.student.insertMany([
  { ID: '00128', name: 'Zhang', dept_name: 'Comp. Sci.', tot_cred: 102 },
  { ID: '12345', name: 'Shankar', dept_name: 'Comp. Sci.', tot_cred: 32 },
  { ID: '19991', name: 'Brandt', dept_name: 'History', tot_cred: 80 },
  { ID: '23121', name: 'Chavez', dept_name: 'Finance', tot_cred: 110 },
  { ID: '44553', name: 'Peltier', dept_name: 'Physics', tot_cred: 56 },
  { ID: '45678', name: 'Levy', dept_name: 'Physics', tot_cred: 46 },
  { ID: '54321', name: 'Williams', dept_name: 'Comp. Sci.', tot_cred: 54 },
  { ID: '55739', name: 'Sanchez', dept_name: 'Music', tot_cred: 38 },
  { ID: '70557', name: 'Snow', dept_name: 'Physics', tot_cred: 0 },
  { ID: '76543', name: 'Brown', dept_name: 'Comp. Sci.', tot_cred: 58 },
  { ID: '76653', name: 'Aoi', dept_name: 'Elec. Eng.', tot_cred: 60 },
  { ID: '98765', name: 'Bourikas', dept_name: 'Elec. Eng.', tot_cred: 98 },
  { ID: '98988', name: 'Tanaka', dept_name: 'Biology', tot_cred: 120 },
]);


# Queries

1 - db.takes.aggregate([
  {
    $lookup: {
      from: "student",
      localField: "ID",
      foreignField: "ID",
      as: "student_info"
    }
  },
  { $unwind: "$student_info" },
  {
    $lookup: {
      from: "teaches",
      localField: "course_id",
      foreignField: "course_id",
      as: "teaches_info"
    }
  },
  { $unwind: "$teaches_info" },
  {
    $lookup: {
      from: "instructor",
      localField: "teaches_info.ID",
      foreignField: "ID",
      as: "instructor_info"
    }
  },
  { $unwind: "$instructor_info" },
  {
    $project: {
      _id: 0,
      student_name: "$student_info.name",
      instructor_name: "$instructor_info.name",
      course_title: "$teaches_info.course_id"
    }
  }
]);



2 - db.instructor.aggregate([
  {
    $lookup: {
      from: "teaches",
      localField: "ID",
      foreignField: "ID",
      as: "teaches_info"
    }
  },
  { $unwind: "$teaches_info" },
  {
    $lookup: {
      from: "section",
      let: {
        course_id: "$teaches_info.course_id",
        sec_id: "$teaches_info.sec_id",
        semester: "$teaches_info.semester",
        year: "$teaches_info.year"
      },
      pipeline: [
        {
          $match: {
            $expr: {
              $and: [
                { $eq: ["$course_id", "$$course_id"] },
                { $eq: ["$sec_id", "$$sec_id"] },
                { $eq: ["$semester", "$$semester"] },
                { $eq: ["$year", "$$year"] }
              ]
            }
          }
        }
      ],
      as: "section_info"
    }
  },
  { $unwind: "$section_info" },
  {
    $lookup: {
      from: "classroom",
      localField: "section_info.building",
      foreignField: "building",
      as: "classroom_info"
    }
  },
  { $unwind: "$classroom_info" },
  {
    $group: {
      _id: {
        professor: "$name",
        building: "$classroom_info.building",
        room_number: "$classroom_info.room_number"
      },
      professor: { $first: "$name" },
      predio: { $first: "$classroom_info.building" },
      sala: { $first: "$classroom_info.room_number" }
    }
  },
  {
    $sort: {
      "professor": 1,
      "predio": 1,
      "sala": 1
    }
  },
  {
    $project: {
      _id: 0,
      professor: 1,
      predio: 1,
      sala: 1
    }
  }
]);

3 - db.department.aggregate([
  {
    $lookup: {
      from: "student",
      localField: "dept_name",
      foreignField: "dept_name",
      as: "students"
    }
  },
  {
    $lookup: {
      from: "instructor",
      localField: "dept_name",
      foreignField: "dept_name",
      as: "instructors"
    }
  },
  {
    $unwind: {
      path: "$students",
      preserveNullAndEmptyArrays: true // equivalent to LEFT JOIN in SQL
    }
  },
  {
    $unwind: {
      path: "$instructors",
      preserveNullAndEmptyArrays: true // equivalent to LEFT JOIN in SQL
    }
  },
  {
    $group: {
      _id: {
        dept_name: "$dept_name",
        budget: "$budget"
      },
      total_alunos: { $addToSet: "$students.ID" },
      salario_medio: { $avg: "$instructors.salary" }
    }
  },
  {
    $project: {
      _id: 0,
      dept_name: "$_id.dept_name",
      orcamento: "$_id.budget",
      total_alunos: { $size: "$total_alunos" },
      salario_medio: 1
    }
  },
  {
    $sort: {
      dept_name: 1
    }
  }
]);



# Conexão

Caso deseje conectar, chave de Connection String para executar no MongoDB Shell: mongodb+srv://bielbolado:Hh7rapbscn@cluster0.ntkvsyl.mongodb.net/?retryWrites=true&w=majority
