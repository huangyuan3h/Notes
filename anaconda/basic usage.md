# Basic usage of anaconda

## 1. check version

```bash
conda -V
```

## 2. do update

```bash
conda update conda

```

## 3. create venv

```bash
conda create -n {name} python={version} anaconda 
```

## 4. active your virtual env

```bash
source active {name}
```

## 5. install package

```bash
conda install -n yourenvname {package}
```

## 6. deactivate

```bash
source deactivate
```

## 7. remove env

```bash
conda remove -n {name} -all
```

## 8. Export env to yml file

```bash
conda env export > env.yml
```

## 9. To reproduce env

```bash

conda env create -f env.yml
```