#import pytoml as toml
import enscons

env = Environment(
    tools=["default", "packaging", enscons.generate],
    PACKAGE_METADATA={
        'name': 'test-enscons',
        'version': '0.1'
    },
    WHEEL_TAG="py2.py3-none-any",
)

py_source = env.Glob("src/test_enscons/*.py")

purelib = env.Whl("purelib", py_source, root="src")
whl = env.WhlFile(purelib)

sdist = env.SDist(source=FindSourceFiles() + ["PKG-INFO"])
env.NoClean(sdist)
env.Alias("sdist", sdist)

develop = env.Command("#DEVELOP", enscons.egg_info_targets(env), enscons.develop)
env.Alias("develop", develop)

env.Default(whl, sdist)
