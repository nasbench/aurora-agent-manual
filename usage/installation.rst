Installation
============

Requirements
------------

Aurora runs on Windows 7 or newer and requires administrative privileges.

Other OS (Linux or macOS) are not supported.

Supported
~~~~~~~~~
- Windows 7 x86 / x64
- Windows Server 2008 R2 x64
- Windows 8.1
- Windows Server 2012
- Windows Server 2012 R2
- Windows 10
- Windows 11
- Windows Server 2016
- Windows Server 2019
- Windows Server 2022

Define an Antivirus / EDR Exclusion
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It is recommended to exclude Aurora from your Antivirus / EDR solution.

Depending on your architecture and whether Aurora was installed or started interactively
from a temporary directory, the exclusion paths are:

1. For an installed Aurora

.. code:: doscon

   C:\Program Files\Aurora-Agent\aurora-agent-64.exe
   C:\Program Files\Aurora-Agent\aurora-agent.exe

2. For a interactively started Aurora the path you have used for extraction. For example:

.. code:: doscon

   C:\aurora\aurora-agent-64.exe
   C:\aurora\aurora-agent.exe

Quick Start
-----------

1. Extract the program package into a temporary folder (e.g. ``C:\aurora``)
2. Make sure to place the ``*.lic`` file into the extracted folder
3. Start a cmd.exe as administrator
4. Navigate to the extracted folder
5. Run the following command 

.. code:: doscon

    C:\aurora>aurora-agent.exe --install

6. Verify that new events arrived in the local "Application" event log (Event Viewer)
7. Run the following commands to get details on the current status of the agent 

.. code:: doscon

    C:\aurora>aurora-agent.exe --status 
    C:\aurora>aurora-agent.exe --status --trace

Manual installation
-------------------

Install Aurora
~~~~~~~~~~~~~~

You can install the agent using the following command line from command line terminal that has been started "As Administrator".

.. code:: doscon

    C:\aurora>aurora-agent.exe --install

After the installation the agent, configuration files and rules reside in ``C:\Program Files\Aurora Agent\``.

It automatically copies all rule files located in the sub-folders ``signatures\sigma-rules`` and ``custom-signatures``.
The ``signatures\sigma-rules`` folder contains the current open source rule set maintained
in the `Sigma repository <https://github.com/SigmaHQ/sigma>`__.
The ``custom-signatures`` folder can be used to add your own sigma rules.

Aurora comes with with 4 configuration presets that we encourage you to explore and use: 

- Standard (``agent-config-standard.yml``)
- Reduced (``agent-config-reduced.yml``)
- Minimal (``agent-config-minimal.yml``)
- Intense (``agent-config-intense.yml``)

The different presets are explained in more detail in the chapter :ref:`usage/configuration:configuration`.

An installation that uses the preset named "reduced" would look like this: 

.. code:: doscon

    C:\aurora>aurora-agent.exe --install -c agent-config-reduced.yml
 
Custom Settings
~~~~~~~~~~~~~~~

Adding your own Sigma rules or IOCs is described in chapter :ref:`usage/custom-signatures:Custom Signatures and IOCs`.
The preferred way is to add them to the ``custom-signatures`` folder before you install Aurora.

All the flags that you use after ``--install`` get written to the configuration file
named ``agent-config.yml`` in the ``C:\Program Files\Aurora Agent\`` folder and will be used by the service.

A typical command to install Aurora would look like this

.. code:: doscon

    C:\aurora>aurora-agent.exe --install --activate-responses

Uninstall Aurora
~~~~~~~~~~~~~~~~

To uninstall the agent simply run the following command:

.. code:: doscon 

    C:\Program Files\Aurora-Agent>aurora-agent.exe --uninstall

If the uninstaller fails due to unknown errors, you can uninstall Aurora manually with these commands (Run from an administrative shell)

.. code:: doscon

    C:\Users\nextron>sc stop aurora-agent 
    C:\Users\nextron>sc delete aurora-agent
    C:\Users\nextron>rmdir /s /q "C:\Program Files\Aurora-Agent"
    C:\Users\nextron>schtasks /Delete /F /TN aurora-agent-program-update
    C:\Users\nextron>schtasks /Delete /F /TN aurora-agent-signature-update

Installation using ASGARD
-------------------------

When using ASGARD Management Center, Aurora can be installed using the ``Service Control`` tab;
see the `relevant chapter in the ASGARD manual <https://asgard-manual.nextron-systems.com/en/latest/usage/administration.html#aurora>`_
for details.
