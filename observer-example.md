# Observer Pattern Example

Let's create a simple web-based notification system using the Observer pattern.

In this example, when a new notification is posted via the input field, all registered devices (observers) will be updated with the new notification.

### HTML

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Observer Pattern Example: Notification System</title>
</head>
<body>
    <input id="notificationInput" type="text" placeholder="Enter notification">
    <button onclick="postNotification()">Post Notification</button>
    <div id="devices">
        <div class="device" id="device1">Device 1: <span></span></div>
        <div class="device" id="device2">Device 2: <span></span></div>
    </div>

    <script>
        class NotificationService {
            constructor() {
                this.observers = [];
            }

            addObserver(observer) {
                this.observers.push(observer);
            }

            removeObserver(observer) {
                const index = this.observers.indexOf(observer);
                if (index !== -1) {
                    this.observers.splice(index, 1);
                }
            }

            notifyObservers(notification) {
                for (let observer of this.observers) {
                    observer.update(notification);
                }
            }
        }

        class Device {
            constructor(elementId) {
                this.element = document.getElementById(elementId);
            }

            update(notification) {
                this.element.querySelector('span').innerText = notification;
            }
        }

        const notificationService = new NotificationService();
        const device1 = new Device('device1');
        const device2 = new Device('device2');
        notificationService.addObserver(device1);
        notificationService.addObserver(device2);

        function postNotification() {
            const notification = document.getElementById('notificationInput').value;
            notificationService.notifyObservers(notification);
        }
    </script>
</body>
</html>
```

**In this example**:

- The `NotificationService` class is the subject that maintains a list of observers and notifies them of new notifications.
- The `Device` class is an observer that updates its display when it receives a new notification.
- Two device instances (`device1` and `device2`) are created and registered with the `NotificationService`.
- When the "Post Notification" button is clicked, the notification is fetched from the input field and passed to the `NotificationService`, which in turn notifies all registered devices.

Loading this HTML in a browser, you can post new notifications, and see them immediately displayed on both devices, demonstrating the Observer pattern in action.