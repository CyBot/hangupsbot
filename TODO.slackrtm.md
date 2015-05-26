# ToDos for the slackrtm plugin

* https://github.com/CyBot/hangupsbot/commit/eee4e4810e9872e32ab9a2d84e7b335264eae6ef : OK, laut Doku ist loop.call_soon_threadsafe() immer noch ein asynchroner Aufruf. Da handle_reply() nix zurück liefern muss ist das eventuell kein Problem. Aber was passiert mit einer in handle_reply() geworfenen Exception? Der bisherige Code hat die ja direkt unter loop.call_soon_threadsafe() gefangen, mit dem asynchronen Aufruf wird das aber doch wohl nicht mehr funktionieren. Falls dem so ist, müssen wir in handle_reply() alle Exceptions fangen und behandeln.
* https://github.com/CyBot/hangupsbot/commit/c449b4ccf5d9df728190589c4b71b481d8ce4e7c : Die 3 Sekunden stammen von python-rtmbot. Kam mir auch kurz vor, aber wenn SlackHQ das in ihrem Beispielcode machen, sollen sie sich nicht beschweren, wenn man das so übernimmt. Bei 30sec ist die Chance auch höher, dass man eine Nachricht verpasst, weil der Server die Verbindung schon geschlossen hat. Das sleep(1) verzögert die Nachrichten auch. Ich arbeite an einer Alternative, die mit polling arbeitet, dass können wir uns das sleep() ganz sparen. Bis dahin würde ich gerne bei sleep(.1) bleiben und aus o.g. Gründen auch bei ping(3).
* https://github.com/CyBot/hangupsbot/commit/c449b4ccf5d9df728190589c4b71b481d8ce4e7c : Effizienter! Aber: der gleichzeitige Zugriff aus verschiedenen Threads muss synchronisiert werden, z.B. update_users()
* https://github.com/CyBot/hangupsbot/commit/bd15cca563049fbf33cee3b349479733c77f43fc : Sicher dass der Type-Cast von Thread zu SlackRTMThread funktioniert?