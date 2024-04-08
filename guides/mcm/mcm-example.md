# Complete JSON Example 
Below is a complete example json structure that showcases all possible options in their glory!! :)

```json
{
    "test": true,
    "meta": {
        "game": false, 
        "vers": "1.0", 
        "auth": "DekitaRPG", 
        "desc": "This is an example for custom mod configuration structure",
        "link": {
            "nexus-mod-id": "577",
            "curse-slug": "miscellaneous/mod-config-menu",
            "donate": "https://www.patreon.com/DekitaRPG"
        }
    },
    "My First Boolean Option": {
        "type": "boolean",
        "init": true,
        "live": true
    },
    "My First Floater Option": {
        "type": "float",
        "init": 0.5,
        "live": 0.5
    },
    "My Custom Boolean": {
        "type": "boolean",
        "desc": "awesome description",
        "flag": "when-server-only",
        "init": true,
        "live": true
    },
    "My Custom Header": {
        "type": "header",
        "desc": "This is a header, it's just for looks."
    },
    "My Custom Integer": {
        "type": "integer",
        "desc": "some description..",
        "flag": "when-server-only",
        "opts": { "min": 69, "max": 420, "step": 2 },
        "init": 69,
        "live": 69
    },
    "My Custom Floater": {
        "type": "float",
        "desc": "some description..",
        "flag": "when-server-only",
        "opts": { "min": 0.25, "max": 0.75, "step": 0.05 },
        "init": 0.5,
        "live": 0.5
    },
    "My Custom String": {
        "type": "string",
        "desc": "some description..",
        "flag": "when-server-only",
        "init": "im the initial text",
        "live": "im live"
    },
    "My Custom Option": {
        "type": "option",
        "desc": "some description.",
        "opts": ["Option 1","Option 2", "Option 3"],
        "init": "Option 2",
        "live": "Option 2"
    },
    "My Custom Color": {
        "type": "color",
        "name": "I'm some custom name shown",
        "reqs": ["My Custom Boolean"],
        "desc": "The text color used for the custom server button",
        "init": { "r": 0.623961, "g": 0.879623, "b": 0.955974, "a": 1 },
        "live": { "r": 0.623961, "g": 0.879623, "b": 0.955974, "a": 1 }
    },
    "My Custom Keybind": {
        "type": "keybind",
        "desc": "This is an example keybind",
        "reqs": ["My Custom Boolean"],
        "init": {"key": "F6","bShift": false,"bCtrl": false,"bAlt": false,"bCmd": false},
        "live": {"key": "F6","bShift": false,"bCtrl": false,"bAlt": false,"bCmd": false}
    }, 
    "My Custom Object": {
        "type": "object",
        "data": {
            "Object Option 1": {
                "type": "boolean",
                "init": true,
                "live": true
            },
            "Object Option 2": {
                "type": "boolean",
                "init": true,
                "live": true
            }
        }
    }
}
```