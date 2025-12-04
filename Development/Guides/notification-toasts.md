
## Server side error generation

Controled errors handled in the backend can be sent to the client and displayed as a toast notification as described in the following example: 

```python
 @method_decorator(require_POST)
    def register_request_action(self, request, pk):
        organization = get_object_or_404(Organization, pk=pk)
        action = request.POST.get("action")
        profile = UserProfile.objects.filter(organization=organization).first()
        if not profile.user.email_verified:
            msg = _(
                "This account email has not been verified yet,contact the user and request email validation before taking further actions."
            )
            response = HttpResponse(
                "",
                headers={
                    "HX-Retarget": "#notifications",
                    "HX-Reswap": "beforeend",
                    "HX-Trigger": '{"notification": {"type": "error","text": "' + msg + '"}}',
                },
            )
            return response

```

Lets breakdown whats going on:

1. First, we check if a condition is met, in order to trigger an error response. In this case, if the user has not verified their email we won't allow the requested action to be triggered.
2. Translate the message to be displayed.
3. Prepare the request with an empty body, hence the use of empty string as first parameter. In this case, we don't want the UI to be updated except for the error toast. To avoid the original swaping (in this case updating a table row), we "retarget" the htmx request to the notifications container, which won't have any visual effect. 
4. Emit an notification event with detail in JSON. This can be tricky, since we are writting JSON ¡its mandatory to use double quotes in the plain text! The "notification" receives an notification object instance which informs two parameters: type (information, error, warning, success) and text (the translated message to be displayed). 
5. The event will be catched by the `#notifications` HTML element that is palced in the default-layout template of both users and admins. Then it'll trigger notificationsStore add method, described under `assets/js/notificationsStore.js`.