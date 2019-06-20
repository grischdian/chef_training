# chef_training

firewall-cmd --zone=public --add-port=443/tcp --permanent
firewall-cmd --zone=public --add-port=80/tcp --permanent
firewall-cmd --reload


Erstellen Sie ein Cookbook das folgende Eigenschaften hat:

- in der metadata.rb die Version auf 0.1.0

- Attributes-File setzt Default Attribute (eines davon als force_override)
  - force_override['aufgabe']['name'] = "Force Override String aus dem Attribute File"
  - default['aufgabe']['environment'] = "Default String aus dem Attribute File"
  - default['aufgabe']['recipe'] = "Default String aus dem Attribute File"
  - default['aufgabe']['role'] = "Default String aus dem Attribute File"

- Default Recipe
  - überschreibt alle Attribute mittels "override" (_NICHT_ force_override)
    => attribute aufgabe::name soll somit immernoch aus attribute file kommen
  - definiert Attribut node.default['aufgabe']['cookbook']['version'] mit dem gleichen wert wie die Version in metadata.rb (0.1.0)
  - Installiert Apache (oder httpd)
  - startet diesen
  - erzeugt aus ERB-Template eine index.html unter /var/www/html/index.html

- ERB-Template
  - greift auf alle 4 Attribute zu und gibt diese aus.

Laden Sie das Cookbook anschließend hoch (knife cookbook upload ..... )
==========================================================================================================

Aufgabe 2:

Ändern Sie nun in der metadata.rb und im recipe/default.rb den Versionsstring ab (z.B 0.1.1)

Laden Sie das Cookbook anschließend erneut hoch (knife cookbook upload ..... )

===========================================================================================================

Aufgabe 3:

Erstellen Sie eine Rolle 'webserver'
  - überschreiben Sie das Attribut "[aufgabe][role] mit dem Wert: ROLLE-WEBSERVER aus Rolle überschrieben

  - run_list: recipe[aufgabe]


Erstellen Sie ein Environment devel

  - überschreibt Attribut [aufgabe][environment] mit "Dieser Server is DEVEL-Spielwiese"
  - Setzt die Cookbook-Version für 'aufgabe' auf den Wert 0.1.1


Erstellen Sie ein Environment prod

  - überschreibt Attribut [aufgabe][environment] mit "Dieser Server ist PROD - KEINE SPIELWIESE"
  - Setzt die Cookbook-Version für 'aufgabe' auf den Wert 0.1.0

==========================================================================================================

Aufgabe 4:

Wenden Sie die Runlist-Rolle 'webserver' auf server1 an und setzten diesen in das devel-environment

 - knife node edit node2

Auf server1: starten Sie 'chef-client' - ergebnis beobachten

ändern Sie das Environment auf prod

 - knife node edit node2

Auf server1: starten Sie 'chef-client' - ergebnis beobachten 

