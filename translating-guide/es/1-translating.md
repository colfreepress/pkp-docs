Introducción
============

OJS y OCS son sistemas multilenguaje, permitiendo a las revistas y conferencias publicar en una variedad de idiomas. El objetivo del Public Knowledge Project es proveer traducciones en inglés, Francés, Español y Portugués tanto para el OJS como para el OCS. Adicionalmente, las traducciones para ambos sistemas han sido realizados por la comunidad, y están bienvenidas las contribuciones todo el tiempo.

Todo el texto que vemos en una típica OxS interfaz ha sido obtenida desde el sistema de código, y ha sido, de hecho, recuperado desde uno o varios  archivos locales de XML. Estos archivos pueden ser encontrados en las carpetas usando un apropiado código ISO (El identificador de código de idioma seguido por el identificador del país), por ejemplo en_US para inglés americano, o pt_BR para portugues brasilero. Este documento usará  en_US para los ejemplos.

Estos directorios locales usualmente tienen archivos en XML que contienen listas de claves de mensajes escritos en ellos. Estas claves y sus correspondientes valores, corresponden a plantilas en un sistema de código propio. El siguiente mensaje está tomado de locale/en_US/locale.xml:

```
<message key="navigation.journalHelp">Journal Help</message>
<message key="navigation.home">Home</message>
<message key="navigation.about">About</message>
<message key="navigation.userHome">User Home</message>
<message key="navigation.login">Log In</message>
<message key="navigation.register">Register</message>
```

Cuando el sistema necesita mostrar una pieza de texto, este primero determina el idioma en el que debe mostrarlo. En primer lugar, se verifica qué idioma ha sido configurado por defecto en todo el sistema por el administrador del sitio. Si los usuarios estan constantemente viendo la revista, el sistema en cambio verifica el idioma que el administrador de la Revista ha dejado cómo predeterminado. Finalmente, si se tienen instalados multiples idiomas, el sistema verifica si los usuarios han especificado otros lenguajes para ser utilizados en vez del predeterminado. Más información sobre la administración de idiomas pueden ser encontrada en la sección sobre verificacion de disponibilidad de idiomas.

![Verificación de idiomas](https://github.com/colfreepress/pkp-docs/blob/master/translating-guide/es/Img/Verificacion%20de%20idiomas.png)

Una vez el sistema conoce el idioma que está viendo el usuario, este graba un valor en el "message key" en el archivo local que pertenece a una traducción específica: que es, si necesita mostrar el texo relevante  key="navigation.journalHelp" proveniente del ejemplo de arriba, y sabemos que debe mostrar el texto en inglés, este se verá en locale/en_US/locale.xml para el valor apropiado de la clave, en este caso "Journal Help". Si el mensaje clave no existe (si el archivo local está perdido, o no existe sobre el sistema en el primer lugar), el sistema mostrará el mensaje clave rodeado por los símbolos de numeral: ##navigation.journalHelp##

Si alguna vez ve este tipo de código en la página de OJS o OCS, debe saber que la traducción está incompleta. Tu puedes ver la sección sobre traducción para saber como se completa.

Revisando la disponibilidad de idiomas
==============================

Se aconseja que primero se verifique cuáles idiomas están disponibles para la versión de OJS o OCS que utliza. Si el lenguaje no está en la lista, entonces verifique la disponibilidad en el sitio web.

Verificando el software para disponibildad de idiomas
----------------------------------------------

En primer lugar, para la  verificación de la disponibilidad de idiomas se debe hacer desde la instalación del software.
Para ambos, OJS y OCS: Si tiene un acceso como administrador al sistema, ingrese y diríjase a la pantalla principal, y de click al link de idiomas, que lo llevará a la página de administración de idiomas. 

Esta página tiene dos secciones principalmente:

-   Under <em>Language Settings</em> you will find a drop-down box for
    your Primary Locale: this sets the default language across the
    entire site; users will be presented with this language by default,
    until they change their own language preference.\
    \
    You will also see a list of supported locales, with checkboxes next
    to them. The selected locales will be available for use by all
    journals hosted on the site, and will also appear in a language
    select menu on each site page (which can be overridden on
    journal-specific pages). If multiple locales are not selected, the
    language toggle menu will not appear and extended language settings
    will not be available to journals.
-   Under Manage Locales you will find a list of installed locales, as
    well as a list of new locales that haven't been installed.\
    \
    Beside each installed locale you will see: a link to <em>reload
    locale</em>, useful if you have made any changes to any locale
    files; and a link to <em>uninstall locale</em>, which will not
    remove locale files from your server but will remove them from the
    list of supported locales.\
    \
    At the very bottom, beside each locale that hasn't yet been
    installed, you will see a checkbox. To install a language, check the
    box next to its name and click <em>Install</em>. The page will
    reload and the locale will appear under <em>Manage Locales</em>.\
    \
    If a language is listed as available and installed from the Site
    Administrator's <em>Languages</em> administration page, you will
    still have to enable it for your journal or conference for it to be
    available to users. Log in as a Journal Manager or Conference
    Manager, and from your User Home click on <em>Languages</em> to
    visit the journal- or conference-specific language administration
    page. Here you will be able to set the primary locale for your
    journal or conference, and likewise enable supported languages to be
    used journal- or conference-wide. If you enable more than one
    language, users will be able to toggle between them via a drop-down
    menu on the sidebar.

Checking the PKP Website for Available Languages
------------------------------------------------

The PKP keeps an up-to-date list of languages and contributors from the
relevant project page.

-   [OJS Languages List](http://pkp.sfu.ca/ojs-languages)

-   [OCS Languages List](http://pkp.sfu.ca/ocs-languages)

Information is organized in a table, with the software version along the
X axis and the list of languages on the Y axis. Clicking on a language
name will take you to an individual language page, which will list the
most recent contributors, and any other relevant information.

All languages fall into the following categories:

-   **Complete:** either bundled with that particular version of OCS or
    OJS, or are otherwise available for download from the list.

-   **Needs Updating:** these files may be included with the version you
    are using (the table will indicate this) but incomplete for some
    reason (they may be a version out of date but still relevant enough
    to be useful; or they may not have been 100% translated in the first
    place). If they are listed as not being included with the software
    version you are using, you can contact the last known maintainers to
    see if they have any recent files.

If you don't see the language(s) you are looking for listed on either of
these lists, please consider undertaking the translation yourself. If
you are interested in contributing in such a way, [contact
us](http://pkp.sfu.ca/contact) for advice, or consult the rest of this
document.

Installing a Language
=====================

Language packs are available in tar.gz archive format, and can be
installed by following these steps (You will require software such as
7-Zip to decompress the downloaded file):

-   Untar the archive to your OJS or OCS root directory on the server:
    this will place the translated locale files into the appropriate
    directories;
-   Add the locale to `registry/locales.xml` using the following syntax:

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE locales SYSTEM "../dbscripts/xml/dtd/locales.dtd">
<locales>
    <locale key="de_DE" name="Deutsch (Deutschland)"/>
    <locale key="en_US" name="English"/>
    <locale key="es_ES" name="Español (España)"/>
    <locale key="fr_CA" name="Français (Canada)"/>
    (... and so on)
</locales>
```

-   Log into your system as a System Administrator, and go to your
    Languages page;
-   Check the checkbox beside the newly-registered locale under Install
    New Locales and click <em>Install</em>;
-   After the page reloads, check the checkbox beside the
    newly-installed locale beside Supported Locales and click
    <em>Save</em>.

You will then need to either visit each conference or journal you are
administering and activate the language from the Journal/Conference
Manager Language page. You can do this by checking the box beside
Supported Locales and clicking <em>Save</em>.

**Warning:** Visit your system information page
(http://<your-site>/index.php/index/admin/systemInfo) and review your
"registry\_dir" variable to be sure you are editing the right
locales.xml


Translation Managers
====================

(explain translation managers)


Translations by Application
===========================

You will find more information on translations, including contributors
and translations notes, below. Contributors are encouraged to [contact
us](mailto:pkp.contact@gmail.com) for login information to maintain
their translation page.

(link to wiki, list of applications' locales)
