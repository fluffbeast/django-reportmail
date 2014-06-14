Advanced topics
===============

In this page, you can learn more about `django-reportmail`.
I'll show you helpful topics when you should address some sort of customising
especially, appearing at your job.

How to change the mail template
-------------------------------

This section you can learn the way to change template used for rendering report mail.
To change the template, you can simply apply the path to template as the 'template' argument
for `apply_template`:

.. code-block:: python

    from django.core.management.base import BaseCommand
    from reportmail.command import apply_reporter

    class Command(BaseCommand):
        @apply_reporter("Title", template='yourapp/dataimport_report.txt')
        def handle(reporter, *args, **options):
            pass

By default, it uses `reportmail/command_report.txt`.

This template will take these values as context:

* stored_text: list of messages you stored.
* args: arguments of command calling.
* options: option arguments of command calling and some value of enviroments.
* command: module path for this command.

If you want to add another value, you can simply set item for the reporter.context atribute:

.. code-block:: python

    >>> reporter.context['some_additional_value'] = 'Hi, there'

How to change the way to report
-------------------------------

Sometimes you want to change the way to report instead of admin mails.
To change, you can simply set a 'Committer' function to the `reporter.committer` attribute.
The committer is the function which to get 'subject' and 'body' string as positional argument
and cause some side-effects:

.. code-block:: python

    >>> def my_committer(subject, body):
    ...     print(subject)
    ...     print(body)
    >>> reporter.committer = my_committer

This my_committer is actually same with `reportmail.reporter.console_committer`.
django-reportmail provides two committer functions by default:

* `reportmail.reporter.console_committer`: printing out to the standard output
* `reportmail.reporter.admin_mail_committer`: sending as admin mail (default committer)

Conclusion
----------

You've already learned about django-reportmail good enough.
If you need some reference for this linbrary, please refer :doc:`api`.
This will useful when you want to remind behaviors of each components.

If you've read whole documentation and have some questions or opinions,
please raise a new issue at
`django-reportmail repository <https://github.com/hirokiky/django-reportmail>`_