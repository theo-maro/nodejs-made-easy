# nodejs-made-easy

This is a comprehensive and up-to-date Node.js course for JavaScript back-end developers

## RESTful Services with Express

Express is a fast and lightweight framework for building web applications

[Home](../README.md) / [RESTful Services](./restful.md) / [Express Web Server](./express.md) / Handling HTTP Requests

### Handling HTTP `GET` Requests

responding to HTTP GET request

- Get all courses

  ```js
  app.get("/api/courses", (req, res) => res.send(courses));
  ```

  Example url : `http://localhost:3000/api/courses`

- Get a specific course by its id

  ```js
  app.get("/api/courses/:id", (req, res) => {
    // look up the course with given id, if not exist return 404
    const course = courses.find(
      (course) => course.id === parseInt(req.params.id)
    );
    if (!course) return res.status(404).send("Course was not found");

    // return the course
    res.send(course);
  });
  ```

  Example url : `http://localhost:3000/api/courses/1`

### Handling HTTP `POST` Requests

responding to a HTTP POST request

- Create a new course

  ```js
  app.post("/api/courses", (req, res) => {
    // validate a course, if invalid return 400
    const { error } = validateCourse(req.body);
    if (error) return res.status(400).send(error.details[0].message);

    // read the course object inside a body of request
    const course = {
      id: courses.length + 1,
      name: req.body.name,
      code: req.body.code,
      price: req.body.price,
      duration: req.body.duration,
    };

    // create new course
    courses.push(course);

    // return created course
    res.send(course);
  });
  ```

  Example url : `http://localhost:3000/api/courses`

### Handling HTTP `PUT` Requests

responding to a HTTP PUT request

- update a course by its id

  ```js
  app.put("/api/courses/:id", (req, res) => {
    // look up the course with given id, if not exist return 404
    const course = courses.find(
      (course) => course.id === parseInt(req.params.id)
    );
    if (!course) return res.status(404).send("Course was not found");

    // validate the course, if invalid return 400
    const { error } = validateCourse(req.body);
    if (error) return res.status(400).send(error.details[0].message);

    // update the course
    course.name = req.body.name;
    course.code = req.body.code;
    course.price = req.body.price;
    course.duration = req.body.duration;

    // return updated course
    res.send(course);
  });
  ```

  Example url : `http://localhost:3000/api/courses/1`

### Handling HTTP `DELETE` Requests

responding to a HTTP DELETE request

- Delete all courses

  ```js
  app.delete("/api/courses", (req, res) => {
    if (!courses) res.status(400).send("No courses");
    courses.splice(0, courses.length);
    res.send(courses);
  });
  ```

  Example url : `http://localhost:3000/api/courses`

- delete specific course by its id

  ```js
  app.delete("/api/courses/:id", (req, res) => {
    // look up the course with given id, if not exist return 404
    const course = courses.find(
      (course) => course.id === parseInt(req.params.id)
    );
    if (!course) return res.status(404).send("Course was not found");

    // delete the course
    const index = courses.indexOf(course);
    courses.splice(index, 1);

    // return deleted course
    res.send(course);
  });
  ```

  Example url : `http://localhost:3000/api/courses/1`
