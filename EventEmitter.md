# EventEmitter Implementation

This document explains the implementation of a custom `EventEmitter` class, similar to the event handling systems found in Node.js or the DOM.

## Implementation

The `EventEmitter` class provides two main methods:

- `subscribe(eventName, callback)`: Registers a callback function for the specified event.
- `emit(eventName, args)`: Triggers all callbacks associated with the specified event and returns their results.

### Code

```javascript
class EventEmitter {
    constructor() {
        this.events = new Map();
    }

    /**
     * Subscribes to an event with a given callback.
     * @param {string} eventName - The name of the event to subscribe to.
     * @param {Function} callback - The callback function to register.
     * @return {Object} An object with an `unsubscribe` method.
     */
    subscribe(eventName, callback) {
        if (!this.events.has(eventName)) {
            this.events.set(eventName, []);
        }
        const listeners = this.events.get(eventName);
        listeners.push(callback);

        return {
            unsubscribe: () => {
                const index = listeners.indexOf(callback);
                if (index !== -1) {
                    listeners.splice(index, 1);
                }
            }
        };
    }

    /**
     * Emits an event, triggering all callbacks registered for that event.
     * @param {string} eventName - The name of the event to emit.
     * @param {Array} [args=[]] - The arguments to pass to each callback.
     * @return {Array} An array of results from each callback invocation.
     */
    emit(eventName, args = []) {
        if (!this.events.has(eventName)) {
            return [];
        }
        const listeners = this.events.get(eventName);
        return listeners.map(callback => callback(...args));
    }
}
