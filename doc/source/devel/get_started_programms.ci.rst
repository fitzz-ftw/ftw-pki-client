The Certificat Sign Request Creation
#########################################




.. SECTION - Setup
>>> test_data_pre= "test_client_data"

>>> from fitzzftw.devtools.testinfra import TestHomeEnvironment
>>> from pathlib import Path
>>> env = TestHomeEnvironment(Path("doc/source/devel/testhome"),
...     appname="ftwpki", appauthor="FitzzTeXnikWelt")
>>> env.setup(True)
>>> env.clean_home()

.. !SECTION - Setup
.. SECTION - Prepare

>>> from pathlib import Path

>>> test_data_dir = "data-client"
>>> config_file = "M-V-HH-Office-1.toml"

>>> conf_file = env.copy2cwd(f"{test_data_dir}/{config_file}", config_file)

>> def stub_getpass(prompt:str)->str:
...     print(prompt)
...     return "strenggeheim"




>>> cmd_line=f"--conf-file {config_file}  "
>>> cmd_line += " -k tim-note"
>>> cmd_line += " -dns tim.member.example.org"
>>> cmd_line += " tim@example.org"

>>> import shlex
>>> sys_argv= shlex.split(cmd_line) 
>>> sys_argv #doctest: +NORMALIZE_WHITESPACE
['--conf-file', 'M-V-HH-Office-1.toml', 
 '-k', 'tim-note', 
 '-dns', 'tim.member.example.org', 
 'tim@example.org']



.. !SECTION - Prepare
>>> from ftwpki.baselibs.workflows import CSRWorkflow
>>> from ftwpki.baselibs.policies import BasePolicy, ClientPolicy

.. SECTION - Start programm

.. SECTION - Configuration
>>> csr_creator = CSRWorkflow()
>>> csr_creator.policy = ClientPolicy()
>>> csr_creator.mandantory_san = True
>>> csr_creator.configuration(sys_argv)


.. !SECTION - Configuration

.. SECTION - CSR Creation

>>> csr_creator.csr_creation()

.. !SECTION - CSR Creation

.. SECTION - Keypair Creation

>>> csr_creator.key_pair_creation()

.. !SECTION - Keypair Creation


.. SECTION - Save private Key
>>> csr_creator.save_keys()

.. !SECTION - Save private Key

.. SECTION - Save CSR
>>> csr_creator.save_csr()


.. !SECTION - Save CSR


.. SECTION - pki- Container
>>> csr_creator.process_pki_container()


.. !SECTION - pki- Container

.. SECTION - Cleanup

>>> csr_creator.cleanup()

.. !SECTION - Cleanup


.. !SECTION - Stop programm

.. SECTION - Test existing keys


>>> conf_path:Path = env.config_dir
>>> public_path:Path = env.data_dir


>>> (conf_path/ ".private" / "tim-note.key.pem").is_file()
True


>>> (public_path / config_file ).with_suffix(".pki").is_file()
True


.. !SECTION - Test existing keys

.. SECTION - Load and read CSR

>>> from ftwpki.baselibs.core import load_csr_from_pem

>>> pki_name = "M-V-HH-Office-1"

>>> csr_obj = load_csr_from_pem(Path(f"{pki_name + '.csr'}").read_bytes()) 

>>> csr_obj #doctest: +ELLIPSIS
<cryptography.hazmat.bindings._rust.x509.CertificateSigningRequest object at ...>

>>> from ftwpki.baselibs.core import get_subject_dict

>>> get_subject_dict(csr_obj) #doctest: +ELLIPSIS +NORMALIZE_WHITESPACE
{'countryName': 'DE', 
 'stateOrProvinceName': '', 
 'localityName': 'Hamburg', 
 'organizationName': 'Muster-Verband e.V.', 
 'organizationalUnitName': 'Mitgliederverwaltung', 
 'commonName': 'Mustermann-Notebook'}

.. !SECTION - Load and read CSR



.. SECTION - Teardown

>>> env.clean_home()
>>> env.teardown()


.. !SECTION - Teardown
