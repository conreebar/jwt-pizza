# Learning notes

## JWT Pizza code study and debugging

As part of `Deliverable ⓵ Development deployment: JWT Pizza`, start up the application and debug through the code until you understand how it works. During the learning process fill out the following required pieces of information in order to demonstrate that you have successfully completed the deliverable.

| User activity                                       | Frontend component | Backend endpoints | Database SQL |
| --------------------------------------------------- | ------------------ | ----------------- | ------------ |
| View home page                                      |                    |none                   |none              |
| Register new user<br/>(t@jwt.com, pw: test)         |                    |'/api/auth', 'POST'  |INSERT INTO user (name, email, password) VALUES (?, ?, ?) INSERT INTO userRole (userId, role, objectId) VALUES (?, ?, ?)              |
| Login new user<br/>(t@jwt.com, pw: test)            |                    |'/api/auth', 'PUT' |INSERT INTO user (name, email, password) VALUES (?, ?, ?) INSERT INTO userRole (userId, role, objectId) VALUES (?, ?, ?) INSERT INTO auth (token, userId) VALUES (?, ?)            |
| Order pizza                                         |                    |     |            |
| Verify pizza                                        |                    |                   |              |
| View profile page                                   |                    |                   |              |
| View franchise<br/>(as diner)                       |                    |                   |              |
| Logout                                              |                    |             '/api/auth', 'DELETE'      | SELECT userId FROM auth WHERE token=  DELETE FROM auth WHERE token=?           |
| View About page                                     |                    |                   |              |
| View History page                                   |                    |                   |              |
| Login as franchisee<br/>(f@jwt.com, pw: franchisee) |                    |  '/api/auth', 'PUT'                 | SELECT * FROM user WHERE email=? SELECT * FROM userRole WHERE userId=? INSERT INTO auth (token, userId) VALUES (?, ?)           |
| View franchise<br/>(as franchisee)                  |                    |/api/franchise/${user.id}                   |  SELECT userId FROM auth WHERE token=? SELECT objectId FROM userRole WHERE role='franchisee' AND userId=?    SELECT id, name FROM franchise WHERE id in (${franchiseIds.join(',')}) SELECT u.id, u.name, u.email FROM userRole AS ur JOIN user AS u ON u.id=ur.userId WHERE ur.objectId=? AND ur.role='franchisee'      |
| Create a store                                      |                    | /api/franchise/${franchise.id}/store`, 'POST'                  | SELECT userId FROM auth WHERE token=?  SELECT u.id, u.name, u.email FROM userRole AS ur JOIN user AS u ON u.id=ur.userId WHERE ur.objectId=? AND ur.role='franchisee'           |
| Close a store                                       |                    |   /api/franchise/${franchise.id}/store/${store.id}`, 'DELETE'                |  SELECT userId FROM auth WHERE token=?      SELECT u.id, u.name, u.email FROM userRole AS ur JOIN user AS u ON u.id=ur.userId WHERE ur.objectId=? AND ur.role='franchisee  DELETE FROM store WHERE franchiseId=? AND id=?  SELECT userId FROM auth WHERE token=? SELECT id, name FROM franchise WHERE id in (${franchiseIds.join(',')}) SELECT u.id, u.name, u.email FROM userRole AS ur JOIN user AS u ON u.id=ur.userId WHERE ur.objectId=? AND ur.role='franchisee' |
| Login as admin<br/>(a@jwt.com, pw: admin)           |                    |  '/api/auth', 'PUT'   | SELECT * FROM user WHERE email=?  SELECT * FROM userRole WHERE userId=?  INSERT INTO auth (token, userId) VALUES (?, ?)             |
| View Admin page                                     |                    |                   |              |
| Create a franchise for t@jwt.com                    |                    |                   |              |
| Close the franchise for t@jwt.com                   |                    |                   |              |
