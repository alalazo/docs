.. _visual_studio_build_environment:


VisualStudioBuildEnvironment
============================

Prepares the needed environment variables to invoke the Visual Studio compiler:

.. code-block:: python
   :emphasize-lines: 3, 4, 5

      def build(self):
         if self.settings.compiler == "Visual Studio":
            env_build = VisualStudioBuildEnvironment(self)
            with tools.environment_append(env_build.vars):
                vcvars = tools.vcvars_command(self.settings)
                self.run('%s && cl /c /EHsc hello.cpp' % vcvars)
                self.run('%s && lib hello.obj -OUT:hello.lib' % vcvars


Set environment variables:

+--------------------+---------------------------------------------------------------------+
| NAME               | DESCRIPTION                                                         |
+====================+=====================================================================+
| LIB                | Library paths separated with ";"                                    |
+--------------------+---------------------------------------------------------------------+
| CL                 | "/I" flags with include directories                                 |
+--------------------+---------------------------------------------------------------------+


**Attributes**

+-----------------------------+---------------------------------------------------------------------+
| PROPERTY                    | DESCRIPTION                                                         |
+=============================+=====================================================================+
| .include_paths              |  List with directories of include paths                             |
+-----------------------------+---------------------------------------------------------------------+
| .lib_paths                  |  List with directories of libraries                                 |
+-----------------------------+---------------------------------------------------------------------+

You can adjust the automatically filled values modifying the attributes above:


.. code-block:: python
   :emphasize-lines: 3, 4, 5

      def build(self):
         if self.settings.compiler == "Visual Studio":
            env_build = VisualStudioBuildEnvironment(self)
            env_build.include_paths.append("mycustom/directory/to/headers")
            env_build.lib_paths.append("mycustom/directory/to/libs")
            with tools.environment_append(env_build.vars):
                vcvars = tools.vcvars_command(self.settings)
                self.run('%s && cl /c /EHsc hello.cpp' % vcvars)
                self.run('%s && lib hello.obj -OUT:hello.lib' % vcvars


.. seealso:: - :ref:`Reference/Tools/environment_append <environment_append_tool>`