import pytoml as toml
import enscons


metadata = dict(toml.load(open("pyproject.toml")))["tool"]["enscons"]

full_tag = "py3-none-any"

env = Environment(
    tools=["default", "packaging", enscons.generate],
    PACKAGE_METADATA=metadata,
    WHEEL_TAG=full_tag,
)

py_source = env.Glob("src/test_enscons/*.py")

purelib = env.Whl("purelib", py_source, root="src")
whl = env.WhlFile(purelib)

# after the wheel
sdist = env.SDist(source=FindSourceFiles() + ["PKG-INFO", "setup.py"])
env.NoClean(sdist)
env.Alias("sdist", sdist)

develop = env.Command("#DEVELOP", enscons.egg_info_targets(env), enscons.develop)
env.Alias("develop", develop)

# needed for pep517 / enscons.api to work
env.Default(whl, sdist)
