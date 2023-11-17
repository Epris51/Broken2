function authUser(req, res, next) {
  try {
    const token = req.body._token || req.query._token;
    if (token) {
      let payload = jwt.decode(token);
      req.curr_username = payload.username;
      req.curr_admin = payload.admin;
    }
    return next();
  } catch (err) {
    err.status = 401;
    return next(err);
  }
}
function authUser(req, res, next) {
  try {
    const token = req.body._token;
    if (token) {
      let payload = jwt.decode(token);
      req.curr_username = payload.username;
      req.curr_admin = payload.admin;
    }
    return next();
  } catch (err) {
    err.status = 401;
    return next(err);
  }
}
/In the updated version, I removed the check for the token in query parameters (req.query._token) to improve security. Now, the middleware only accepts tokens from the request body (req.body._token). This change ensures that tokens are not exposed in URLs or logs, enhancing security.

router.post('/login', async function(req, res, next) {
  try {
    const { username, password } = req.body;
    let user = User.authenticate(username, password);
    const token = createTokenForUser(username, user.admin);
    return res.json({ token });
  } catch (err) {
    return next(err);
  }
}); // end

router.post('/login', async function(req, res, next) {
  try {
    const { username, password } = req.body;
    let user = await User.authenticate(username, password);
    const token = createTokenForUser(username, user.admin);
    return res.json({ token });
  } catch (err) {
    return next(err);
  }
}); // end
Execution Flow: The function User.authenticate(username, password) is now called with await. This instructs the JavaScript engine to pause execution at this line until the Promise returned by User.authenticate is resolved or rejected.
Improved Behavior:
Correct Data Handling: By awaiting the promise, user will be the actual user object after User.authenticate resolves, allowing correct access to user.admin.
Error Handling: If User.authenticate throws an error, it will now be caught by the try...catch block, improving the robustness of error handling.

router.delete('/:username', authUser, requireAdmin, async function(
  req,
  res,
  next
) {
  try {
    User.delete(req.params.username);
    return res.json({ message: 'deleted' });
  } catch (err) {
    return next(err);
  }
}); // end

router.delete('/:username', authUser, requireAdmin, async function(
  req,
  res,
  next
) {
  try {
    await User.delete(req.params.username);
    return res.json({ message: 'deleted' });
  } catch (err) {
    return next(err);
  }
}); // end

Explanation:
Execution Flow: By using await User.delete(req.params.username), the execution of the function pauses at this line until the Promise returned by User.delete is resolved or rejected.
Improved Behavior:
Complete Operation: The await ensures that the user deletion process completes before sending the response. This means the client gets a response only after the user is successfully deleted.
Better Error Handling: If User.delete throws an error, it will be caught by the try...catch block. This allows for proper error handling and communication of any issues to the client.

app.use(function(err, req, res, next) {
  res.status(err.status || 500);

  app.use(function(req, res, next) {
  res.status(404).json({
    status: 404,
    message: "Not Found"
  });
});

In this updated version, the 404 response is sent directly from the 404 handler middleware.
Benefits:
Simplicity and Efficiency: This approach simplifies the flow by directly returning the 404 response without needing to involve the general error handler.
Clear Intent: It makes the code more readable and its intent clearer, as the 404 response handling is self-contained within its own middleware.


module.exports = app;

The code was included twice, the redundant code was deleted.

