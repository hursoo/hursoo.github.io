---
layout: single
title: "[23파이썬특강] 2강. 데이터 프레임과 분석 기초(코드)"
author_profile: false
toc : true
---

<head>
  <style>
    table.dataframe {
      white-space: normal;
      width: 70%;
      height: 240px;
      display: block;
      overflow: auto;
      font-family: Arial, sans-serif;
      font-size: 0.9rem;
      line-height: 20px;
      text-align: center;
      border: 0px !important;
    }

    table.dataframe th {
      text-align: center;
      font-weight: bold;
      padding: 8px;
    }

    table.dataframe td {
      text-align: center;
      padding: 8px;
    }

    table.dataframe tr:hover {
      background: #b8d1f3; 
    }

    .output_prompt {
      overflow: auto;
      font-size: 0.9rem;
      line-height: 1.45;
      border-radius: 0.3rem;
      -webkit-overflow-scrolling: touch;
      padding: 0.8rem;
      margin-top: 0;
      margin-bottom: 15px;
      font: 1rem Consolas, "Liberation Mono", Menlo, Courier, monospace;
      color: $code-text-color;
      border: solid 1px $border-color;
      border-radius: 0.3rem;
      word-break: normal;
      white-space: pre;
    }

  .dataframe tbody tr th:only-of-type {
      vertical-align: middle;
  }

  .dataframe tbody tr th {
      vertical-align: top;
  }

  .dataframe thead th {
      text-align: center !important;
      padding: 8px;
  }

  .page__content p {
      margin: 0 0 0px !important;
  }

  .page__content p > strong {
    font-size: 0.8rem !important;
  }

  </style>
</head>


# <span style="color:blue; font-weight:bold;">2강. 데이터 프레임과 분석 기초</span>

- 둘째마당 (04-05)

- pp.074-130 (57쪽)



```python
# 그래프 해상도 설정
import matplotlib.pyplot as plt
plt.rcParams.update({'figure.dpi' : '100'})
%config InlineBackend.figure_format = 'retina'
```


```python
"""
[챗지피티] 2023/12/09
matplotlib이라는 단어의 출처는? -----
"Matplotlib"이라는 단어는 파이썬의 시각화 라이브러리의 이름에서 유래. 
"Matplotlib"의 이름은 "MATLAB"이라는 또 다른 기술적 컴퓨팅 환경과 언어에서 영감을 받아서 만들어짐.
MATLAB은 과학 계산과 시각화를 위한 인기 있는 플랫폼.
따라서 "Matplotlib"은 MATLAB의 그래픽 기능을 표현하는 "MAT"과 파이썬의 "Plotting library"를 결합한 이름.
* "Plotting library"란 데이터 시각화를 위해 사용되는 소프트웨어 라이브러리. 
   과학적, 교육적, 비즈니스 분석 등 다양한 분야에서 데이터의 패턴, 추세, 관계를 이해하고 설명하는 데 널리 사용.
"""
```


```python
import seaborn  # 패키지 로드
```


```python
var = ['a', 'a', 'b', 'c']
var
```

<pre>
['a', 'a', 'b', 'c']
</pre>

```python
import seaborn as sns
```


```python
"""
[챗지피티] 2023/12/03
Seaborn이라는 파이썬 데이터 시각화 라이브러리는 
"웨스트 윙(The West Wing)"이라는 텔레비전 쇼에 등장하는 
가상 인물인 Samuel Norman Seaborn의 이름을 따서 명명되었습니다. 
이 캐릭터는 배우 Rob Lowe가 연기했으며, 
문제에 대해 분석적이고 체계적인 접근 방식으로 알려져 있습니다. 
이는 Seaborn 라이브러리가 목표로 하는 매력적이고 유익한 
통계 그래픽을 그리기 위한 고급 인터페이스를 제공하는 것과 일치합니다. 
이러한 명명법은 프로그래밍 커뮤니티에서 소프트웨어와 라이브러리를 
대중 문화 참조로 이름 짓는 경향을 반영합니다.
"""
```


```python
seaborn.countplot(x = var)
```

<pre>
<Axes: ylabel='count'>
</pre>
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABIAAAAM6CAYAAAD5XjjHAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjcuMiwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8pXeV/AAAACXBIWXMAAB7CAAAewgFu0HU+AABd/ElEQVR4nO3de5RX1X03/vcXcOQOIiogk4h3rMaqgIl4ARM0RvAW8RKiYjWPeaJNbDUmMRGx1afQKonpE60GFdGgqMsgghWiVVSCBWwiqGhiIgqIKAiiDMhtfn/4Yx6Q2wDDDJx5vdaatTbfs89nfya4Js7bc/YuVVZWVgYAAACAwmpQ1w0AAAAAsH0JgAAAAAAKTgAEAAAAUHACIAAAAICCEwABAAAAFJwACAAAAKDgBEAAAAAABScAAgAAACg4ARAAAABAwQmAAAAAAApOAAQAAABQcAIgAAAAgIITAAEAAAAUnAAIAAAAoOAEQAAAAAAFJwACAAAAKLhGdd0AO4dly5Zl+vTpSZI99tgjjRr5RwcAAABq2sqVK/PBBx8kSQ477LA0bty4Rur6LZ5qmT59erp161bXbQAAAEC9MXny5HTt2rVGankFDAAAAKDgPAFEteyxxx5V48mTJ6d9+/Z12A0AAAAU09y5c6vewFn7d/FtJQCiWtbe86d9+/bp2LFjHXYDAAAAxVeT++96BQwAAACg4ARAAAAAAAUnAAIAAAAoOAEQAAAAQMEJgAAAAAAKTgAEAAAAUHACIAAAAICCEwABAAAAFJwACAAAAKDgBEAAAAAABScAAgAAACg4ARAAAABAwQmAAAAAAApOAAQAAABQcAIgAAAAgIITAAEAAAAUnAAIAAAAoOAEQAAAAAAFJwACAAAAKDgBEAAAAEDBCYAAAAAACk4ABAAAAFBwAiAAAACAgqu3AdD//M//5P/8n/+TU045JeXl5dl1113TvHnzHHjggenfv3+ef/75Gl/zwQcfzMknn5z27duncePG2WeffXLBBRfkxRdfrHaNBQsW5Prrr8/hhx+eVq1apWXLljn88MNz/fXXZ8GCBTXeMwAAALDzK1VWVlbWdRO17YQTTshzzz232XkXXHBBhg4dmrKysm1ab9myZenbt2/GjBmzwesNGjTIwIEDc911122yzpQpU3L66adn7ty5G7zeoUOHPPbYY+nSpcs29bshs2fPTnl5eZJk1qxZ6dixY42vAQAAAPXd9vr9u14+ATRnzpwknwUmP/jBD/LII49k8uTJmTRpUoYMGZK99947SXLfffelf//+27zeJZdcUhX+9OzZM6NGjcrkyZNz1113Zb/99svq1aszYMCADB06dJM99+nTJ3Pnzk2jRo1yzTXX5Lnnnstzzz2Xa665Jo0aNcq7776b3r17V31/AAAAAEk9fQKod+/eufDCC/PNb34zDRs2XO/6/Pnz07179/zpT39Kkjz33HM57rjjtmqtCRMmpEePHkmSPn365Le//e06a86fPz9HHXVU3nnnney2227561//mtatW69Xp3///rn33nuTJA899FD69u27zvWHH34455xzTpLk4osvzt13371V/W6MJ4AAAABg+/MEUA0aM2ZMzjnnnA2GP0nStm3b3HLLLVV/fuSRR7Z6rX/9139NkjRs2DC33Xbbemu2bds2gwcPTpIsXLgwd91113o15s2bl/vvvz9JcvLJJ68X/iRJ3759c/LJJydJhg8fnnnz5m11zwAAAECx1MsAqDrWPLWTJH/5y1+2qsYnn3ySp59+OknSq1evjaZ2Z511Vlq2bJkkefTRR9e7Pnr06KxatSrJZ0/3bMya19VWrVqV0aNHb1XPAAAAQPEIgDZi+fLlVeMGDbbuf6bJkyfn008/TfLZxtMbU1ZWli9/+ctV96xYsWKd62ufSLapOmtfe+GFF7aqZwAAAKB4BEAbMWHChKrxwQcfvFU1ZsyYUe0aa66vXLkyf/7znzdYp1WrVmnXrt1Ga7Rv377qSaK11wYAAADqt0Z13cCOaPXq1Rk0aFDVn9dsrrylZs2aVTXe3KZNazZ4WnPfIYccsl6d6mz8VF5enldffXWdtatj9uzZm7y+saPnAQAAgB2fAGgDfv7zn2fy5MlJkjPPPDNdunTZqjoff/xx1bh58+abnNusWbOq8SeffLLBOpursXadz9fYnLUDKAAAAKBYBECfM2HChPz4xz9Okuy55565/fbbt7rWsmXLqsZlZWWbnLvrrrtWjZcuXbrBOpursXadz9cokqN+OLyuWwB2YC/924V13QIAAOxwBEBrefXVV3PmmWdm5cqV2XXXXfPQQw9lr7322up6jRs3rhqvvan0hqzZLDpJmjRpsl6dioqKzdZYu87na2zO5l4Zmzt3brp167ZFNQEAAIAdgwDo//fWW2/lpJNOysKFC9OwYcM88MADmzxxqzpatGhRNd7cK1lLliypGn/+Va8WLVqkoqKiWq91ralTndfF1lad/YUAAACAnZNTwJK8++67+drXvpZ33303pVIpd999d84888xtrrt2qLK5TZbXfgLn8/vxrKmzuRpr17GnDwAAALBGvQ+A5s+fn169euWvf/1rkuTf//3fc+GFNbN/xNoneb3++uubnLvmeqNGjbL//vtvsM5HH32U9957b6M15s6dm8WLFydJOnfuvFU9AwAAAMVTrwOgjz76KCeffHJee+21JMmgQYNy+eWX11j9rl27Vm3cPGHChI3OW758eV588cX17lnj2GOPrRpvqs7a17p3775VPQMAAADFU28DoIqKipx66qn5n//5nyTJT3/60/zoRz+q0TVatGiRr371q0mSp556aqOvcD366KNVT+5s6NWz0047LQ0afPZXdc8992x0vWHDhiVJGjRokNNOO21bWgcAAAAKpF4GQMuXL8+ZZ56ZiRMnJkl+8IMf5MYbb9ziOsOGDUupVEqpVMrAgQM3OOfqq69OkqxcuTKXX355Vq1atc71+fPnVwVPrVu3zqWXXrpejXbt2qVfv35JknHjxuWRRx5Zb87DDz+ccePGJUkuuOCCtGvXbou/HwAAAKCY6uUpYOeff37Gjx+fJDnxxBNzySWX5JVXXtno/LKyshx44IFbtdaJJ56Y8847Lw8++GBGjx6dXr165corr0yHDh0yffr03HTTTXnnnXeSfPYK2m677bbBOjfddFOefPLJfPDBBzn//PMzderU9O7dO0kyZsyY3HLLLUmSPfbYY6vCLAAAAKC46mUA9Oijj1aN/+u//itf+tKXNjn/i1/8YmbOnLnV6919991ZvHhxnnjiiTzzzDN55pln1rneoEGDXHfddbnssss2WqO8vDyPP/54zjjjjLz33nsZPHhwBg8evM6cdu3aZdSoUY50BwAAANZRL18Bq21NmjTJ2LFj85vf/Ca9evXKnnvumbKyspSXl+db3/pWXnjhhY2+Qra2o48+OtOnT8/PfvazHHrooWnevHmaN2+eww47LD/72c/yyiuv5Oijj97+3xAAAACwUylVVlZW1nUT7Phmz56d8vLyJMmsWbPq9Cmjo344vM7WBnZ8L/3bhXXdAgAAbLXt9fu3J4AAAAAACk4ABAAA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8MEHmTBhQiZMmJDBgwdn2LBhOf300zd436xZs5IkHTt23Owa5eXlefXVV6vuqa7Zs2dv8vrnj54HAAAAdh4CoFpw2GGH5Ywzzki3bt3SoUOHrFixIm+88UZ+85vfZPz48Vm0aFG++c1v5vHHH88pp5yy3v0ff/xxkqR58+abXatZs2ZJkk8++WSLeiwvL9+i+QAAAMDOQwC0nV155ZUZOHDgep8fffTRufDCC3PHHXfku9/9blatWpVLL700b775Zpo0abLO3GXLliVJysrKNrverrvumiRZunTptjcPAAAAFIIAaDtr3br1Jq9fdtllmTp1aoYOHZp33303jz76aPr167fOnMaNG6eioiLLly/f7HqffvppkqwXIm3O5l4Zmzt3brp167ZFNQEAAIAdgwBoB3DZZZdl6NChSZIJEyasFwC1aNEiFRUV1Xqta8mSJUmq97rY2qqzvxAAAACwc3IK2A7gkEMOqRrPmTNnvetrwpnNbdSc/L8neezpAwAAAKwhANoBVFZWbvL6moDoo48+ynvvvbfReXPnzs3ixYuTJJ07d665BgEAAICdmgBoB/Daa69VjTt06LDe9WOPPbZqPGHChI3WWfta9+7da6g7AAAAYGcnANoB3HHHHVXjE044Yb3rp512Who0+Oyv6p577tlonWHDhiVJGjRokNNOO61mmwQAAAB2WgKgbTBs2LCUSqWUSqUNHvU+ffr0vPnmm5uscccdd+Suu+5KkrRr1y5nnnnmenPatWtXtTH0uHHj8sgjj6w35+GHH864ceOSJBdccEHatWu3pd8OAAAAUFD19hSwF154YZ1wZv78+VXjN998s+ppmjX69++/xWu89NJLufTSS9OzZ8+ccsopOeyww7L77rtn5cqVef3113P//ffnd7/7XZKkYcOGueOOO9KsWbMN1rrpppvy5JNP5oMPPsj555+fqVOnpnfv3kmSMWPG5JZbbkmS7LHHHrnxxhu3uFcAAACguOptADR06NDce++9G7w2ceLETJw4cZ3PtiYASpJVq1blqaeeylNPPbXRObvvvnvuuuuuTb62VV5enscffzxnnHFG3nvvvQwePDiDBw9eZ067du0yatQoR7oDAAAA66i3AVBt+MY3vpG77rorkyZNyh/+8IfMmzcvCxYsSGVlZdq0aZPDDz88X//619O/f/+0bNlys/WOPvroTJ8+PbfeemtGjRqVmTNnJkk6deqU008/PVdeeWV233337fxdAQAAADubUuXmziCHJLNnz055eXmSZNasWXX6lNFRPxxeZ2sDO76X/u3Cum4BAAC22vb6/dsm0AAAAAAFJwACAAAAKDgBEAAAAEDBCYAAAAAACk4ABAAAAFBwAiAAAACAghMAAQAAABScAAgAAACg4ARAAAAAAAUnAAIAAAAoOAEQAAAAQMEJgAAAAAAKTgAEAAAAUHACIAAAAICCEwABAAAAFJwACAAAAKDgBEAAAAAABScAAgAAACg4ARAAAABAwQmAAAAAAApOAAQAAABQcAIgAAAAgIITAAEAAAAUnAAIAAAAoOAEQAAAAAAFJwACAAAAKDgBEAAAAEDBCYAAAAAACk4ABAAAAFBwAiAAAACAghMAAQAAABScAAgAAACg4ARAAAAAAAUnAAIAAAAoOAEQAAAAQMEJgAAAAAAKTgAEAAAAUHACIAAAAICCEwABAAAAFJwACAAAAKDgBEAAAAAABScAAgAAACg4ARAAAABAwQmAAAAAAApOAAQAAABQcAIgAAAAgIITAAEAAAAUnAAIAAAAoOAEQAAAAAAFJwACAAAAKDgBEAAAAEDBCYAAAAAACk4ABAAAAFBwAiAAAACAghMAAQAAABScAAgAAACg4ARAAAAAAAUnAAIAAAAoOAEQAAAAQMEJgAAAAAAKTgAEAAAAUHACIAAAAICCEwABAAAAFJwACAAAAKDgBEAAAAAABScAAgAAACi4ehsAvf/++xkzZkwGDBiQU045JW3btk2pVEqpVEr//v1rbJ3FixfnwQcfzHe+850ceeSRad26dcrKyrLHHnukR48eufnmm7No0aLN1tlnn32q+tvU1z777FNjvQMAAADF0KiuG6gre+2113Zf4z//8z9z5pln5tNPP13v2vz58zNhwoRMmDAhN998cx544IH07Nlzu/cEAAAA1D/1NgBaW3l5eTp37pzx48fXaN0FCxbk008/TYMGDdKrV698/etfz+GHH57WrVtn9uzZ+c1vfpORI0dm3rx56d27dyZOnJi//du/3WTN008/PTfeeONGr5eVldXo9wAAAADs/OptADRgwIB07do1Xbt2zV577ZWZM2emU6dONbrGLrvskssuuyzXXnttvvCFL6xz7YgjjkifPn3SvXv3fP/7309FRUWuuuqqPP3005us2bp16xx66KE12icAAABQbPU2ALrhhhu2+xrnnntuzj333E3O+fu///sMHz48U6dOzbPPPpsFCxZk99133+69AQAAAPVHvd0EekfSo0ePJMnq1avz1ltv1W0zAAAAQOEIgHYAa28S3aCBvxIAAACgZkkbdgATJkxIkjRq1Cj777//Juc+99xz+dKXvpRmzZqladOm6dSpU84999yMGjUqlZWVtdEuAAAAsJOpt3sA7SjGjh2badOmJUlOPvnktGzZcpPzP/+K2MyZMzNz5sw89NBD6d69e0aOHJm99957i/uYPXv2Jq/PnTt3i2sCAAAAOwYBUB368MMPc/nllydJGjZsmH/+53/e6NyysrKcdtppOemkk3LooYemVatWWbRoUSZNmpTbb789s2bNysSJE9OrV69MmjQprVq12qJeysvLt+l7AQAAAHZcAqA6smrVqvTr1y9vv/12kuRnP/tZjjjiiI3Onzx5clq3br3e5z169MgVV1yRs88+O+PHj8+MGTNyww03ZMiQIdurdQAAAGAnIwCqI9/73vfy5JNPJklOPfXUXHfddZucv6HwZ40WLVrkoYceyn777ZcFCxbkzjvvzKBBg1JWVlbtfmbNmrXJ63Pnzk23bt2qXQ8AAADYcQiA6sBPfvKT3HnnnUmSY489Ng8//HAaNmy4TTVbtWqV8847L7/61a+yZMmSTJ06Ncccc0y17+/YseM2rQ8AAADsuJwCVssGDx6cQYMGJUmOPPLIjBkzJk2aNKmR2occckjVeM6cOTVSEwAAANj5CYBq0W233ZYf//jHSZLOnTtn3LhxW7xZ86Y4Bh4AAADYEAFQLbnvvvtyxRVXJEn23XffPPXUU2nbtm2NrvHaa69VjTt06FCjtQEAAICdlwCoFjz66KO5+OKLU1lZmY4dO+bpp5+u8YDmo48+ysiRI5MkTZs2TZcuXWq0PgAAALDzEgBtg2HDhqVUKqVUKmXgwIEbnDN+/Picf/75WbVqVfbcc8889dRT2WeffbZonSeffDJLly7d6PWPP/4455xzThYsWJAkueSSS7Lrrrtu0RoAAABAcdXbU8BeeOGFvPnmm1V/nj9/ftX4zTffzLBhw9aZ379//y1e48UXX8yZZ56Z5cuXZ5dddsnPf/7zrFixIq+88spG7+nYseN6R74PGjQo/fr1y1lnnZVjjz02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7ty5adSoUa655po899xzee6553LNNdekUaNGeffdd9O7d+/MmTNnu30vAAAAwM6nVp8A2pEMGDAgXbt2TdeuXbPXXntl5syZ6dSpU42vM2HChIwYMSJJ0qdPn/z2t7+t2gy7a9euOe2003LUUUflnXfeyTXXXJOzzz47rVu3Xq/OT3/608ybNy9JMmLEiPTt27fq2nHHHZcuXbrknHPOybx583Ldddfl7rvvrvHvBQAAANg51WkANG/evDz77LN55ZVX8uGHHyZJ2rRpk0MPPTQ9evTYrq9p3XDDDdut9tr+9V//NclnJ6Dddttt652E1rZt2wwePDjnn39+Fi5cmLvuuitXXXXVOnPmzZuX+++/P0ly8sknrxP+rNG3b9+cfPLJGTduXIYPH55/+Zd/qdXX3AAAAIAdV50EQHPnzs0//uM/5tFHH83KlSs3OKdhw4Y5++yzc8stt6R9+/a13GHN+OSTT/L0008nSXr16pWOHTtucN5ZZ52Vli1bZvHixXn00UfXC4BGjx6dVatWJUkuvvjija7Xv3//jBs3LqtWrcro0aPzne98p4a+EwAAAGBnVut7AL388sv50pe+lIceeigrVqzY6BHwK1euzMiRI3P44Ydn+vTptd1mjZg8eXI+/fTTJMkJJ5yw0XllZWVVp4BNnjw5K1asWOf6888/XzXeVJ21r73wwgtb1TMAAABQPLUaAC1ZsiSnnnpqFixYkMrKynzta1/LyJEjM3PmzCxbtizLli3LzJkz89BDD+Wkk05KZWVl5s+fn1NPPTUVFRW12WqNmDFjRtX44IMP3uTcNddXrlyZP//5zxus06pVq7Rr126jNdq3b5+WLVuutzYAAABQv9XqK2D/9//+37z77rtp0KBB7rjjjlxyySXrzfnCF76QL3zhCzn77LNz99135zvf+U7mzJmTX/3qV/nhD39Ym+1us1mzZlWNN/b61xrl5eXr3HfIIYesV2dzNdbUefXVV9dZuzpmz569yeufP3oeAAAA2HnUagD02GOPpVQqpX///hsMfz7v7/7u7/L73/8+d999d37729/udAHQxx9/XDVu3rz5Juc2a9asavzJJ59ssM7maqxd5/M1NmftAAoAAAAolloNgP70pz8lSc4777xq33P++efn7rvvrrp3Z7Js2bKqcVlZ2Sbn7rrrrlXjpUuXbrDO5mqsXefzNQCoX975p8PqugVgB/aFATvnHps1rfu/d6/rFoAd1MS/n1jXLdS4Wg2A1jyV0qZNm2rfs9tuuyX5bP+gnU3jxo2rxsuXL9/k3DWbRSdJkyZN1qtTUVGx2Rpr1/l8jc3Z3Ctjc+fOTbdu3baoJgAAALBjqNUAaI899si7776bGTNm5Mgjj6zWPWs2M27btu32bG27aNGiRdV4c69krR1wff5VrxYtWqSioqJar3WtqVOd18XWVp39hQAAAICdU62eAvblL385lZWVGTJkSFauXLnZ+StWrMgtt9ySUqlUdUz6zmTtUGVzmyyv/QTO5/fjWVNnczXWrmNPHwAAAGCNWg2ALrzwwiTJH//4x5x66ql59913Nzp3zpw56d27d/74xz8mSfr3718LHdastU/yev311zc5d831Ro0aZf/9999gnY8++ijvvffeRmvMnTs3ixcvTpJ07tx5q3oGAAAAiqdWXwHr06dPzjjjjIwaNSpPPfVU9t133/Tq1StHH3109tprr5RKpbz33nv57//+7/zud7/LihUrkiRnnnlmTj311NpstUZ07do1ZWVlWb58eSZMmJAf//jHG5y3fPnyvPjii+vcs7Zjjz029913X5JkwoQJOffcczdYZ8KECVXj7t1taAcAAAB8plYDoCR54IEHcuGFF+bhhx/O8uXL88QTT+SJJ55Yb15lZWWSpG/fvhk+fHhtt1kjWrRoka9+9av5z//8zzz11FOZPXv2BvfaefTRR6ue3DnzzDPXu37aaaflf//v/53Vq1fnnnvu2WgANGzYsCRJgwYNctppp9XcNwIAAADs1Gr1FbDks2PKR44cmccffzynnHJKmjRpksrKynW+mjRpklNOOSVjxozJyJEj1zkifUcybNiwlEqllEqlDBw4cINzrr766iTJypUrc/nll2fVqlXrXJ8/f35+9KMfJUlat26dSy+9dL0a7dq1S79+/ZIk48aNyyOPPLLenIcffjjjxo1LklxwwQVp167dVn9fAAAAQLHU+hNAa5x66qk59dRTs2rVqvz1r3/Nhx9+mOSzI+L33XffNGzYcLuu/8ILL+TNN9+s+vP8+fOrxm+++WbV0zRrbO0eRCeeeGLOO++8PPjggxk9enR69eqVK6+8Mh06dMj06dNz00035Z133kmSDBo0qOrY+8+76aab8uSTT+aDDz7I+eefn6lTp6Z3795JkjFjxuSWW25J8tlJazfeeONW9QoAAAAUU50FQGs0bNgwBxxwQK2vO3To0Nx7770bvDZx4sRMnDhxnc+2ZRPqu+++O4sXL84TTzyRZ555Js8888w61xs0aJDrrrsul1122UZrlJeX5/HHH88ZZ5yR9957L4MHD87gwYPXmdOuXbuMGjXKke4AAADAOmo1APr444/z85//PEnyv/7X/9rsa0pz587Nr3/96yTJD3/4wzRp0mS797g9NGnSJGPHjs2IESMybNiwvPzyy1m0aFH22muvHHfccbniiivyla98ZbN1jj766EyfPj233nprRo0alZkzZyZJOnXqlNNPPz1XXnlldt999+383QAAAAA7m1Llmt2Wa8F9992Xiy66KAcccEDeeOONzc6vrKzMwQcfnDfffDMPPPBAzjnnnFrokg2ZPXt2ysvLkySzZs2q06eMjvrhzrkpOFA7Xvq3C+u6hR3CO/90WF23AOzAvjBgel23sEPo/u9OzgU2bOLfT9z8pO1ke/3+XaubQD/66KMplUrVDnJKpVLOO++8VFZW5uGHH97O3QEAAAAUU60GQK+//nqS5Jhjjqn2PWtejXrttde2S08AAAAARVerAdDs2bOTJO3bt6/2PWv2CZozZ8526QkAAACg6Go1AGrQ4LPlKioqqn3PmrkrV67cLj0BAAAAFF2tBkBrnvyZOnVqte9ZM3dzJ4YBAAAAsGG1GgAdd9xxqayszG233ZYVK1Zsdv6KFSty2223pVQq5dhjj62FDgEAAACKp1YDoIsvvjhJ8uc//znf+ta3NvkqWEVFRc4///z86U9/WudeAAAAALZMo9pc7Jhjjsl5552XBx98MI8++mj++7//O9/5zndy/PHHp3379imVSnn33Xfz3HPPZejQoZk9e3ZKpVLOPvvsnHDCCbXZKgAAAEBh1GoAlCR333135s+fn6eeeipz5szJwIEDNzivsrIySdKrV6/ce++9tdghAAAAQLHU6itgSdK4ceOMGzcuP//5z9OhQ4dUVlZu8Ku8vDy//OUv8+STT6Zx48a13SYAAABAYdT6E0BJUiqV8oMf/CDf//7388c//jF/+MMfMn/+/CRJ27Ztc+SRR+bwww9PqVSqi/YAAAAACqVOAqA1SqVSjjjiiBxxxBF12QYAAABAodX6K2AAAAAA1C4BEAAAAEDBCYAAAAAACk4ABAAAAFBwAiAAAACAghMAAQAAABScAAgAAACg4ARAAAAAAAUnAAIAAAAoOAEQAAAAQMEJgAAAAAAKTgAEAAAAUHACIAAAAICCEwABAAAAFJwACAAAAKDgBEAAAAAABScAAgAAACg4ARAAAABAwQmAAAAAAApOAAQAAABQcAIgAAAAgIITAAEAAAAUnAAIAAAAoOAEQAAAAAAFJwACAAAAKDgBEAAAAEDBCYAAAAAACk4ABAAAAFBwAiAAAACAghMAAQAAABScAAgAAACg4ARAAAAAAAUnAAIAAAAoOAEQAAAAQMEJgAAAAAAKTgAEAAAAUHACIAAAAICCEwABAAAAFJwACAAAAKDgBEAAAAAABScAAgAAACg4ARAAAABAwQmAAAAAAApOAAQAAABQcAIgAAAAgIITAAEAAAAUnAAIAAAAoOAEQAAAAAAFJwACAAAAKDgBEAAAAEDBCYAAAAAACk4ABAAAAFBwAiAAAACAghMAAQAAABScACjJO++8k6uvvjqdO3dOs2bN0qZNm3Tr1i0333xzKioqtrrus88+m1KptEVfPXr02GCtffbZp1r377PPPlvdLwAAAFBMjeq6gbo2duzY9OvXLx999FHVZxUVFZkyZUqmTJmSoUOH5oknnsi+++5bK/0cdNBBtbIOAAAAUH/U6wDo5ZdfzjnnnJOKioo0b948P/nJT9KzZ88sXbo0Dz74YH7961/njTfeyKmnnpopU6akefPmW1S/a9eumT59+mbnXXHFFZkwYUKS5KKLLtrk3NNPPz033njjRq+XlZVtUY8AAABA8dXrAOjKK69MRUVFGjVqlPHjx+crX/lK1bUTTzwxBxxwQK655pq8/vrrGTJkSAYMGLBF9Zs1a5ZDDz10k3MWLVqUF198MUmy//7755hjjtnk/NatW2+2JgAAAMDa6u0eQFOmTMmzzz6bJLnkkkvWCX/WuOqqq9K5c+ckyS9+8YusWLGixvsYOXJkPv300yTJBRdcUOP1AQAAAOptADRq1Kiq8cUXX7zBOQ0aNMiFF16YJFm4cGFVYFSThg8fniQplUoCIAAAAGC7qLcB0PPPP5/ks9e0jjrqqI3OO+GEE6rGL7zwQo328Je//CW///3vkyTHHXdcOnXqVKP1AQAAAJJ6HADNmDEjyWf77jRqtPGtkA4++OD17qkpa57+STa/+fMazz33XL70pS+lWbNmadq0aTp16pRzzz03o0aNSmVlZY32BwAAABRDvdwEetmyZZk/f36SpGPHjpucu9tuu6VZs2ZZsmRJZs2aVaN93H///UmSJk2a5Oyzz67WPW+99dY6f545c2ZmzpyZhx56KN27d8/IkSOz9957b3Evs2fP3uT1uXPnbnFNAAAAYMdQLwOgjz/+uGpcnaPd1wRAn3zySY318Pzzz+evf/1rkuTMM89My5YtNzm/rKwsp512Wk466aQceuihadWqVRYtWpRJkybl9ttvz6xZszJx4sT06tUrkyZNSqtWrbaon/Ly8q3+XgAAAIAdW70MgJYtW1Y1Lisr2+z8XXfdNUmydOnSGuvhvvvuqxqv2Wh6UyZPnpzWrVuv93mPHj1yxRVX5Oyzz8748eMzY8aM3HDDDRkyZEiN9QoAAADs3OplANS4ceOq8fLlyzc7f80x7U2aNKmR9T/99NM8/PDDSZIOHTrka1/72mbv2VD4s0aLFi3y0EMPZb/99suCBQty5513ZtCgQdUKt9bY3Ottc+fOTbdu3apdDwAAANhx1MsAqEWLFlXj6rzWtWTJkiTVe12sOh577LEsWrQoSdKvX780bNhwm2u2atUq5513Xn71q19lyZIlmTp1ao455phq37+5vZAAAACAnVe9PAWscePGadu2bZLNb368cOHCqgCopvbJWfv0r+q8/lVdhxxySNV4zpw5NVYXAAAA2LnVywAoSTp37pwkefPNN7Ny5cqNznv99dfXu2dbvP/++xk3blyS5Mgjj8yhhx66zTXXcAw8AAAAsCH1NgA69thjk3z2etdLL7200XkTJkyoGnfv3n2b1x0xYkRV4FSTT/8kyWuvvVY17tChQ43WBgAAAHZe9TYAOuOMM6rG99xzzwbnrF69uup1rdatW6dnz57bvO6aeo0aNcq3vvWtba63xkcffZSRI0cmSZo2bZouXbrUWG0AAABg51ZvA6Bu3brluOOOS5LcddddmTRp0npzbrnllsyYMSNJ8oMf/CC77LLLOteHDRuWUqmUUqmUgQMHbnbNV199NX/4wx+SJKecckr22GOPavX65JNPbvII+o8//jjnnHNOFixYkCS55JJLqo6uBwAAAKiXp4Ctceutt6Z79+5ZunRpTjrppFx77bXp2bNnli5dmgcffDB33nlnkuTAAw/MVVddtc3r3XvvvVXjiy66qNr3DRo0KP369ctZZ52VY489Nvvtt1+aN2+eRYsWZdKkSbn99turjnE/6KCDqhVGAQAAAPVHvQ6AjjjiiIwcOTLf/va3s3jx4lx77bXrzTnwwAMzduzYdY6O3xqrV6/OiBEjkiS77bZbevfuvUX3f/jhhxk6dGiGDh260TnHH398RowYkTZt2mxTrwAAAECx1OsAKEn69OmTadOm5dZbb83YsWMze/bslJWVZf/990/fvn1zxRVXpGnTptu8ztNPP111NPu55567Ra9o3XzzzXn66aczadKkvPHGG5k/f34WLVqUpk2bpkOHDjn66KNz/vnn56STTkqpVNrmXgEAAIBiqfcBUJJ88YtfzJAhQzJkyJAtuq9///7p379/teb26tVrq49p79Kli02dAQAAgK1WbzeBBgAAAKgvBEAAAAAABScAAgAAACg4ARAAAABAwQmAAAAAAApOAAQAAABQcAIgAAAAgIITAAEAAAAUnAAIAAAAoOAEQAAAAAAFJwACAAAAKDgBEAAAAEDBCYAAAAAACk4ABAAAAFBwAiAAAACAghMAAQAAABScAAgAAACg4ARAAAAAAAUnAAIAAAAoOAEQAAAAQMEJgAAAAAAKTgAEAAAAUHACIAAAAICCEwABAAAAFJwACAAAAKDgBEAAAAAABScAAgAAACg4ARAAAABAwQmAAAAAAApOAAQAAABQcAIgAAAAgIITAAEAAAAUnAAIAAAAoOAEQAAAAAAFJwACAAAAKDgBEAAAAEDBCYAAAAAACk4ABAAAAFBwAiAAAACAghMAAQAAABScAAgAAACg4ARAAAAAAAUnAAIAAAAoOAEQAAAAQMEJgAAAAAAKTgAEAAAAUHACIAAAAICCEwABAAAAFJwACAAAAKDgBEAAAAAABScAAgAAACg4ARAAAABAwQmAAAAAAApOAAQAAABQcAIgAAAAgIITAAEAAAAUnAAIAAAAoOAEQAAAAAAFJwACAAAAKDgBEAAAAEDBCYAAAAAACk4ABAAAAFBwAiAAAACAghMAAQAAABScAAgAAACg4ARAAAAAAAUnAEryzjvv5Oqrr07nzp3TrFmztGnTJt26dcvNN9+cioqKbao9cODAlEqlan09++yzm623YMGCXH/99Tn88MPTqlWrtGzZMocffniuv/76LFiwYJt6BQAAAIqpUV03UNfGjh2bfv365aOPPqr6rKKiIlOmTMmUKVMydOjQPPHEE9l3333rsMvPTJkyJaeffnrmzp27zufTpk3LtGnTMnTo0Dz22GPp0qVLHXUIAAAA7IjqdQD08ssv55xzzklFRUWaN2+en/zkJ+nZs2eWLl2aBx98ML/+9a/zxhtv5NRTT82UKVPSvHnzbVpv+vTpm7zeqVOnjV6bM2dO+vTpk3nz5qVRo0b5x3/8x/Tu3TtJMmbMmAwZMiTvvvtuevfunZdeeil77733NvUKAAAAFEe9DoCuvPLKVFRUpFGjRhk/fny+8pWvVF078cQTc8ABB+Saa67J66+/niFDhmTAgAHbtN6hhx661ff+9Kc/zbx585IkI0aMSN++fauuHXfccenSpUvOOeeczJs3L9ddd13uvvvubeoVAAAAKI56uwfQlClTqvbcueSSS9YJf9a46qqr0rlz5yTJL37xi6xYsaI2W6wyb9683H///UmSk08+eZ3wZ42+ffvm5JNPTpIMHz68KiwCAAAAqLcB0KhRo6rGF1988QbnNGjQIBdeeGGSZOHChdXapHl7GD16dFatWpVk470mSf/+/ZMkq1atyujRo2ujNQAAAGAnUG8DoOeffz5J0qxZsxx11FEbnXfCCSdUjV944YXt3teGrOk1Wbefz9sRegUAAAB2PPU2AJoxY0aSZP/990+jRhvfCunggw9e756t1atXr+y+++4pKyvLnnvumR49emTQoEFZuHBhtXpt1apV2rVrt9F57du3T8uWLWukVwAAAKA46uUm0MuWLcv8+fOTJB07dtzk3N122y3NmjXLkiVLMmvWrG1a96mnnqoaf/DBB5kwYUImTJiQwYMHZ9iwYTn99NM3eN+adTfXa5KUl5fn1Vdf3eJeZ8+evcnrnz96HgAAANh51MsA6OOPP64aV+do9zUB0CeffLJV6x122GE544wz0q1bt3To0CErVqzIG2+8kd/85jcZP358Fi1alG9+85t5/PHHc8opp2y03+r2mmSLey0vL9+i+QAAAMDOo14GQMuWLasal5WVbXb+rrvumiRZunTpFq915ZVXZuDAget9fvTRR+fCCy/MHXfcke9+97tZtWpVLr300rz55ptp0qTJBvvd3r0CAAAAxVQvA6DGjRtXjZcvX77Z+Z9++mmSrBfMVEfr1q03ef2yyy7L1KlTM3To0Lz77rt5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znv99dfXu2dr3Xbbbfnxj39cVWvcuHFbvFnzpjgGHgAAANiQehsAHXvssUk+e73rpZde2ui8CRMmVI27d+++1evdd999ueKKK5Ik++67b5566qmqp5BqymuvvVY17tChQ43WBgAAAHZe9TYAOuOMM6rG99xzzwbnrF69OsOHD0/y2SbMPXv23Kq1Hn300Vx88cWprKxMx44d8/TTT9d4QPPRRx9l5MiRSZKmTZumS5cuNVofAAAA2HnV2wCoW7duOe6445Ikd911VyZNmrTenFtuuSUzZsxIkvzgBz/ILrvsss71YcOGpVQqpVQqZeDAgRtcZ/z48Tn//POzatWq7Lnnnnnqqaeyzz77bFGvTz755CaPoP/4449zzjnnZMGCBUmSSy65pOroegAAAIB6eQrYGrfeemu6d++epUuX5qSTTsq1116bnj17ZunSpXnwwQerTuo68MADc9VVV21x/RdffDFnnnlmli9fnl122SU///nPs2LFirzyyisbvadjx47rHfk+aNCg9OvXL2eddVaOPfbY7LfffmnevHkWLVqUSZMm5fbbb686xv2ggw7aaBgFAAAA1E/1OgA64ogjMnLkyHz729/O4sWLc+21164358ADD8zYsWPXOTq+up588slUVFQkSVasWJF+/fpt9p577rkn/fv3X+/zDz/8MEOHDs3QoUM3eu/xxx+fESNGpE2bNlvcKwAAAFBc9ToASpI+ffpk2rRpufXWWzN27NjMnj07ZWVl2X///dO3b99cccUVadq0aZ32ePPNN+fpp5/OpEmT8sYbb2T+/PlZtGhRmjZtmg4dOuToo4/O+eefn5NOOimlUqlOewUAAAB2PKVKZ4dTDbNnz055eXmSZNasWenYsWOd9XLUD4fX2drAju+lf7uwrlvYIbzzT4fVdQvADuwLA6bXdQs7hO7/vvWn/ALFNvHvJ9bZ2tvr9+96uwk0AAAAQH0hAAIAAAAoOAEQAAAAQMEJgAAAAAAKTgAEAAAAUHACIAAAAICCEwABAAAAFJwACAAAAKDgBEAAAAAABScAAgAAACg4ARAAAABAwQmAAAAAAApOAAQAAABQcAIgAAAAgIITAAEAAAAUnAAIAAAAoOAEQAAAAAAFJwACAAAAKDgBEAAAAEDBCYAAAAAACk4ABAAAAFBwAiAAAACAghMAAQAAABScAAgAAACg4ARAAAAAAAUnAAIAAAAoOAEQAAAAQMEJgAAAAAAKTgAEAAAAUHACIAAAAICCEwABAAAAFJwACAAAAKDgBEAAAAAABScAAgAAACg4ARAAAABAwQmAAAAAAApOAAQAAABQcAIgAAAAgIITAAEAAAAUnAAIAAAAoOAEQAAAAAAFJwACAAAAKDgBEAAAAEDBCYAAAAAACk4ABAAAAFBwAiAAAACAghMAAQAAABScAAgAAACg4ARAAAAAAAUnAAIAAAAoOAEQAAAAQMEJgAAAAAAKTgAEAAAAUHACIAAAAICCEwABAAAAFJwACAAAAKDgBEAAAAAABScAAgAAACg4ARAAAABAwQmAAAAAAApOAAQAAABQcAIgAAAAgIITAAEAAAAUnAAIAAAAoOAEQAAAAAAFJwACAAAAKDgBUJJ33nknV199dTp37pxmzZqlTZs26datW26++eZUVFTU2DoPPvhgTj755LRv3z6NGzfOPvvskwsuuCAvvvhitWssWLAg119/fQ4//PC0atUqLVu2zOGHH57rr78+CxYsqLFeAQAAgOJoVNcN1LWxY8emX79++eijj6o+q6ioyJQpUzJlypQMHTo0TzzxRPbdd9+tXmPZsmXp27dvxowZs87nb7/9dt5+++2MGDEiAwcOzHXXXbfJOlOmTMnpp5+euXPnrvP5tGnTMm3atAwdOjSPPfZYunTpstW9AgAAAMVTr58Aevnll3POOefko48+SvPmzXPTTTfl97//fZ5++ul85zvfSZK88cYbOfXUU/PJJ59s9TqXXHJJVfjTs2fPjBo1KpMnT85dd92V/fbbL6tXr86AAQMydOjQjdaYM2dO+vTpk7lz56ZRo0a55ppr8txzz+W5557LNddck0aNGuXdd99N7969M2fOnK3uFQAAACieev0E0JVXXpmKioo0atQo48ePz1e+8pWqayeeeGIOOOCAXHPNNXn99dczZMiQDBgwYIvXmDBhQkaMGJEk6dOnT37729+mYcOGSZKuXbvmtNNOy1FHHZV33nkn11xzTc4+++y0bt16vTo//elPM2/evCTJiBEj0rdv36prxx13XLp06ZJzzjkn8+bNy3XXXZe77757i3sFAAAAiqnePgE0ZcqUPPvss0k+e0Jn7fBnjauuuiqdO3dOkvziF7/IihUrtnidf/3Xf02SNGzYMLfddltV+LNG27ZtM3jw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Z2T48OFZvHhxXbcINaJUWVlZWddNAFTHs88+m549e2523o9//OP8y7/8Sy10BLBjGThwYG644YYkyV//+tf06tUrf/nLXzY49+yzz84DDzyQRo0a1WaLADuMpUuX5pJLLskDDzywyXnXX399Bg4cWDtNwXbk//GBncbKlSvTrFmznHrqqTnxxBNz8MEHp2XLlnn//ffz6quv5pe//GXefvvtDBo0KAceeGAuvvjium4ZoM6ce+65eeutt/Ld7343Z599dlq1apVp06Zl8ODB+dOf/pRHHnkk7du3zy9/+cu6bhWg1q1evTqnn356fve73yVJDjjggHzve99Lly5d0rRp08ydOze///3v89BDD9Vxp1BzPAEE7DTmz5+fRo0apXXr1hu8vnz58vTu3Tu/+93v8sUvfjF/+ctf0rBhw9ptEqAOrf0EUJKMGDEi559//jpzPv744xx33HF5+eWX06BBg/zxj3/MYYcdVtutAtSpW2+9NVdeeWWS5Mwzz8wDDzyQXXfddb15q1evznvvvZcOHTrUcodQ8+wBBOw02rZtu9HwJ0nKysryb//2b0mSt99+O3/84x9rpzGAHVDv3r3XC3+SpEWLFrnzzjuTfPaLzX/8x3/UdmsAdWr16tVV/8649957Z/jw4RsMf5KkQYMGwh8KwytgwE7r008/zbx58/LJJ59k9erVSZK1H2p8+eWXc9RRR9VVewB1alOvwXbr1i1/8zd/k1dffTVPPfVULXYFUPf++Mc/Zs6cOUmS73znO2nevHkddwS1QwAE7FSWLFmSX/7yl3nwwQfz6quvZtWqVRudO3/+/FrsDGDH0rVr101e79atW1599dX8+c9/zvLly1NWVlZLnQHUrT/84Q9V4+OPP74OO4HaJQACdhozZ87MiSeemLfeeqta85cuXbqdOwLYce25556bvL7XXnsl+ezJyYULF1b9GaDo1v6PhO3bt6/DTqB22QMI2GlccMEFeeutt1IqlfJ3f/d3GT9+fGbNmpVly5alsrIylZWV6zwRZI97oD4rlUqbvO5nJMDmf1ZCkXgCCNgpvP7663nhhReSJD/5yU9y0003bXDewoULa7MtgB3WvHnzUl5evtHr77//fpLPfvnZbbfdaqstgDrXtm3bqvG7776bgw46qA67gdrjCSBgp/Dqq69Wjc8777yNzps6dWpttAOww5syZUq1rh9wwAH2/wHqlSOPPLJq/Nxzz9VhJ1C7BEDATmHlypVV44qKio3Oc5wxwGfuvffejV6bOnVqXnnllSTJ1772tdpqCWCHcPjhh1c9ITl06NB88sknddwR1A4BELBTOOCAA6rGG/ul5vbbb8+oUaNqqSOAHdvo0aPz0EMPrff5J598kv/1v/5XkqRBgwa57LLLars1gDrVoEGD/PCHP0ySzJ49OxdeeGGWL1++wbmrV6/Ou+++W5vtwXZjDyBgp3DEEUfk0EMPzSuvvJLbb789ixYtSr9+/dK+ffvMmjUr999/fx555JF07949EydOrOt2Aepcly5d8q1vfSsTJkzI2WefnZYtW2batGkZPHhw3njjjSTJ5Zdfni996Ut13ClA7bv88svz+OOP53e/+11++9vf5rDDDsv3vve9dOnSJU2bNs17772XF198MQ888EC+9a1vZeDAgXXdMmwzARCwUyiVSrnvvvty4oknZuHChXnggQfywAMPrDPnsMMOy8MPP5wOHTrUUZcAO46HHnooX/3qV3PbbbfltttuW+/6N7/5zQwZMqQOOgOoew0aNMioUaNy0UUX5ZFHHsmf/vSnXHnllXXdFmxXXgEDdhp/+7d/mz/+8Y/57ne/my9+8YvZZZdd0qZNm3Tr1i0333xzJk+enPbt29d1mwA7hE6dOuWll17Ktddem86dO6dp06Zp1apVjj/++KqnJhs18t8CgfqradOmefjhh/Nf//VfueCCC9KpU6c0adIkLVq0yMEHH5yzzjorI0aMqHpdDHZ2pcrKysq6bgIAAACA7ccTQAAAAAAFJwACAAAAKDgBEAAAAEDBCYAAAAAACk4ABAAAAFBwAiAAAACAghMAAQAAABScAAgAAACg4ARAAAAAAAUnAAIAAAAoOAEQAAAAQMEJgAAAAAAKTgAEAAAAUHACIAAAAICCEwABAAAAFJwACAAAAKDgBEAAAAAABScAAgAAACg4ARAAAABAwQmAAAAAAApOAAQAAABQcAIgAAAAgIITAAEAAAAUnAAIAAAAoOD+P7RZpXE9WbdgAAAAAElFTkSuQmCC"/>


```python
df = sns.load_dataset('titanic')
df
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>survived</th>
      <th>pclass</th>
      <th>sex</th>
      <th>age</th>
      <th>sibsp</th>
      <th>parch</th>
      <th>fare</th>
      <th>embarked</th>
      <th>class</th>
      <th>who</th>
      <th>adult_male</th>
      <th>deck</th>
      <th>embark_town</th>
      <th>alive</th>
      <th>alone</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>7.2500</td>
      <td>S</td>
      <td>Third</td>
      <td>man</td>
      <td>True</td>
      <td>NaN</td>
      <td>Southampton</td>
      <td>no</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>71.2833</td>
      <td>C</td>
      <td>First</td>
      <td>woman</td>
      <td>False</td>
      <td>C</td>
      <td>Cherbourg</td>
      <td>yes</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>3</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>7.9250</td>
      <td>S</td>
      <td>Third</td>
      <td>woman</td>
      <td>False</td>
      <td>NaN</td>
      <td>Southampton</td>
      <td>yes</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>53.1000</td>
      <td>S</td>
      <td>First</td>
      <td>woman</td>
      <td>False</td>
      <td>C</td>
      <td>Southampton</td>
      <td>yes</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>8.0500</td>
      <td>S</td>
      <td>Third</td>
      <td>man</td>
      <td>True</td>
      <td>NaN</td>
      <td>Southampton</td>
      <td>no</td>
      <td>True</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>886</th>
      <td>0</td>
      <td>2</td>
      <td>male</td>
      <td>27.0</td>
      <td>0</td>
      <td>0</td>
      <td>13.0000</td>
      <td>S</td>
      <td>Second</td>
      <td>man</td>
      <td>True</td>
      <td>NaN</td>
      <td>Southampton</td>
      <td>no</td>
      <td>True</td>
    </tr>
    <tr>
      <th>887</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>19.0</td>
      <td>0</td>
      <td>0</td>
      <td>30.0000</td>
      <td>S</td>
      <td>First</td>
      <td>woman</td>
      <td>False</td>
      <td>B</td>
      <td>Southampton</td>
      <td>yes</td>
      <td>True</td>
    </tr>
    <tr>
      <th>888</th>
      <td>0</td>
      <td>3</td>
      <td>female</td>
      <td>NaN</td>
      <td>1</td>
      <td>2</td>
      <td>23.4500</td>
      <td>S</td>
      <td>Third</td>
      <td>woman</td>
      <td>False</td>
      <td>NaN</td>
      <td>Southampton</td>
      <td>no</td>
      <td>False</td>
    </tr>
    <tr>
      <th>889</th>
      <td>1</td>
      <td>1</td>
      <td>male</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>30.0000</td>
      <td>C</td>
      <td>First</td>
      <td>man</td>
      <td>True</td>
      <td>C</td>
      <td>Cherbourg</td>
      <td>yes</td>
      <td>True</td>
    </tr>
    <tr>
      <th>890</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>32.0</td>
      <td>0</td>
      <td>0</td>
      <td>7.7500</td>
      <td>Q</td>
      <td>Third</td>
      <td>man</td>
      <td>True</td>
      <td>NaN</td>
      <td>Queenstown</td>
      <td>no</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
<p>891 rows × 15 columns</p>
</div>

<br>

# 04. 데이터 프레임의 세계로


## 04-1. 데이터 프레임 이해하기(77-80쪽)

- 데이터는 어떻게 생겼나?


- '열'은 속성(변수), '행'은 한 사람[혹은 한 단위]의 정보

- 한 사람의 정보는 가로 한 줄에 나열

- 데이터가 '크다' = 행 또는 열이 '많다'

- 행 보다 '열'이 많은 것이 더 중요

- 빅데이터보다 다양한 데이터가 더 중요


## 04-2. 데이터 프레임 만들기(81-84쪽)


### [Do it! 실습] 데이터 입력해 데이터 프레임 만들기(81쪽)



```python
import pandas as pd
```


```python
# '딕셔너리' 형식('{}')의 데이터를 이용해서 만들기
## -> 딕셔너리에 관하여는 교재 '17-5. 딕셔너리'(418-421쪽) 참조

df = pd.DataFrame({'name':['김지훈', '이유진', '박동현', '김민지'],
                   'english':[90, 80, 60, 70],
                   'math':[50, 60, 100, 20]})                      # DataFrame -> D, F가 대문자
df
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>english</th>
      <th>math</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>김지훈</td>
      <td>90</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>이유진</td>
      <td>80</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>박동현</td>
      <td>60</td>
      <td>100</td>
    </tr>
    <tr>
      <th>3</th>
      <td>김민지</td>
      <td>70</td>
      <td>20</td>
    </tr>
  </tbody>
</table>
</div>


### [Do it! 실습] 데이터 프레임으로 분석하기(82쪽)


#### 특정 변수의 값 추출하기



```python
df['english']
```

<pre>
0    90
1    80
2    60
3    70
Name: english, dtype: int64
</pre>

#### 변수의 값으로 합계 구하기



```python
sum(df['english'])
```

<pre>
300
</pre>

```python
sum(df['math'])
```

<pre>
230
</pre>

#### 변수의 값으로 평균 구하기



```python
sum(df['english']) / 4
```

<pre>
75.0
</pre>

```python
sum(df['math']) / 4
```

<pre>
57.5
</pre>

### [개인 실습] 혼자서 해보기(84쪽)


### Q1

다음 표의 내용을 데이터 프레임으로 만들어 출력해 보세요

| 제품  | 가격  | 판매량 |
|:-----:|:-----:|:------:|
| 사과  | 1800  |   24   |
| 딸기  | 1500  |   38   |
| 수박  | 3000  |   13   |


##### A1



```python
fruit = pd.DataFrame({'제품':['사과', '딸기', '수박'],
              '가격':[1800, 1500, 3000],
              '판매량':[24, 38, 13]
             })
fruit
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>제품</th>
      <th>가격</th>
      <th>판매량</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>사과</td>
      <td>1800</td>
      <td>24</td>
    </tr>
    <tr>
      <th>1</th>
      <td>딸기</td>
      <td>1500</td>
      <td>38</td>
    </tr>
    <tr>
      <th>2</th>
      <td>수박</td>
      <td>3000</td>
      <td>13</td>
    </tr>
  </tbody>
</table>
</div>


#### Q2

- 앞에서 만든 데이터 프레임을 이용해 과일의 가격 평균과 판매량 평균을 구하라

##### A2


```python
fruit_average_price = sum(fruit['가격']) / 3
fruit_average_price
```

<pre>
2100.0
</pre>

```python
fruit_average_quantity = sum(fruit['판매량']) / 3
fruit_average_quantity
```

<pre>
25.0
</pre>


## 04-3. 외부 데이터 이용하기(85-92쪽)

- 축적된 시험 성적 데이터를 불러오자!

 
### [Do it! 실습] 엑셀 파일 불러오기(85쪽)


#### 엑셀 파일 살펴보기

- 깃허브에서 다운로드 (-> 교재 14쪽 참고)


#### 워킹 디렉토리에 엑셀 파일 삽입하기



```python
import pandas as pd

df_exam = pd.read_excel('excel_exam.xlsx')
df_exam
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
    </tr>
  </tbody>
</table>
</div>



```python
sum(df_exam['english']) / 20
```

<pre>
84.9
</pre>

```python
sum(df_exam['science']) / 20
```

<pre>
59.45
</pre>

```python
# len 사용
x = [1, 2, 3, 4, 5]
len(x)

df = pd.DataFrame({'a':[1,2,3],
                   'b':[4,5,6]
                  })
df
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>



```python
len(df)
```

<pre>
3
</pre>

```python
len(df_exam)
```

<pre>
20
</pre>

```python
sum(df_exam['english']) / len(df_exam)
```

<pre>
84.9
</pre>

```python
sum(df_exam['science']) / len(df_exam)
```

<pre>
59.45
</pre>

```python
# 엑셀 파일의 첫 번째 행이 변수명이 아니라면?

df_exam_novar = pd.read_excel('excel_exam_novar.xlsx')
df_exam_novar
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>1</th>
      <th>1.1</th>
      <th>50</th>
      <th>98</th>
      <th>50.1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
    </tr>
    <tr>
      <th>4</th>
      <td>6</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
    </tr>
    <tr>
      <th>5</th>
      <td>7</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>6</th>
      <td>8</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>



```python
df_exam_novar = pd.read_excel('excel_exam_novar.xlsx', header=None)
df_exam_novar
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>



```python
# CSV 파일 불러오기

df_csv_exam = pd.read_csv('exam.csv')
df_csv_exam
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
    </tr>
  </tbody>
</table>
</div>



```python
# CSV 파일 저장하기

df_midterm = pd.DataFrame({'english':[90, 80, 60, 70],
                           'math':[50, 60, 100, 20],
                           'nclass':[1, 1, 2, 2]})
df_midterm
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>english</th>
      <th>math</th>
      <th>nclass</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>90</td>
      <td>50</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>80</td>
      <td>60</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>60</td>
      <td>100</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>70</td>
      <td>20</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



```python
df_midterm.to_csv('output_newdata.csv', index = False) # index = False
```


```python
# 다시 불러오기

reload = pd.read_csv('output_newdata.csv') # index_col = 0 (위에서 인덱스까지 저장했을 경우)
reload
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>english</th>
      <th>math</th>
      <th>nclass</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>90</td>
      <td>50</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>80</td>
      <td>60</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>60</td>
      <td>100</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>70</td>
      <td>20</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




# 05. 데이터 분석 기초


## 05-1. 데이터 파악하기(99-106쪽)

- head(), tail(), shape, info(), describe()



```python
import pandas as pd
exam = pd.read_csv('exam.csv')
exam
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
    </tr>
  </tbody>
</table>
</div>



```python
exam.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
    </tr>
  </tbody>
</table>
</div>



```python
exam.head(10)
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
    </tr>
  </tbody>
</table>
</div>



```python
exam.tail()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
    </tr>
  </tbody>
</table>
</div>



```python
exam.tail(10)
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
    </tr>
  </tbody>
</table>
</div>



```python
exam.shape
```

<pre>
(20, 5)
</pre>

```python
exam.info()
```

<pre>
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 20 entries, 0 to 19
Data columns (total 5 columns):
 #   Column   Non-Null Count  Dtype
---  ------   --------------  -----
 0   id       20 non-null     int64
 1   nclass   20 non-null     int64
 2   math     20 non-null     int64
 3   english  20 non-null     int64
 4   science  20 non-null     int64
dtypes: int64(5)
memory usage: 932.0 bytes
</pre>

```python
exam.describe()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>20.00000</td>
      <td>20.000000</td>
      <td>20.000000</td>
      <td>20.000000</td>
      <td>20.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>10.50000</td>
      <td>3.000000</td>
      <td>57.450000</td>
      <td>84.900000</td>
      <td>59.450000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>5.91608</td>
      <td>1.450953</td>
      <td>20.299015</td>
      <td>12.875517</td>
      <td>25.292968</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.00000</td>
      <td>1.000000</td>
      <td>20.000000</td>
      <td>56.000000</td>
      <td>12.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>5.75000</td>
      <td>2.000000</td>
      <td>45.750000</td>
      <td>78.000000</td>
      <td>45.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>10.50000</td>
      <td>3.000000</td>
      <td>54.000000</td>
      <td>86.500000</td>
      <td>62.500000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>15.25000</td>
      <td>4.000000</td>
      <td>75.750000</td>
      <td>98.000000</td>
      <td>78.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>20.00000</td>
      <td>5.000000</td>
      <td>90.000000</td>
      <td>98.000000</td>
      <td>98.000000</td>
    </tr>
  </tbody>
</table>
</div>


[용어] 사분위  

- 사분위간 범위 : 제1 사분위수와 제3 사분위수 간의 거리(Q3-Q1)로, 데이터의 중간 50%에 대한 범위

- https://support.minitab.com/ko-kr/minitab/20/help-and-how-to/graphs/boxplot/interpret-the-results/quartiles/

- 그래프 속 위치 <br> 

 <img src='j_lab_imge/image_quantile.PNG' alt='test' style='width: 250px'/>



```python
# mpg 데이터 불러오기.  
'''
cf) mpg : mpg(Mile Per Gallon) 데이터는 
미국 환경 보호국(US Environmental Protection Agency)에서 공개한 자료로, 
1999~2008년 사이 미국에서 출시된 자동차 234종의 연비 관련 정보를 담고 있다.
https://m.blog.naver.com/eunha4685/221496862666
'''
mpg = pd.read_csv('mpg.csv')
mpg
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>18</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>1</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>2</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>20</td>
      <td>31</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>3</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(av)</td>
      <td>f</td>
      <td>21</td>
      <td>30</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>4</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>229</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>19</td>
      <td>28</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>230</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>231</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>232</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>18</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>233</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>3.6</td>
      <td>2008</td>
      <td>6</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>17</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
  </tbody>
</table>
<p>234 rows × 11 columns</p>
</div>



```python
mpg.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>18</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>1</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>2</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>20</td>
      <td>31</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>3</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(av)</td>
      <td>f</td>
      <td>21</td>
      <td>30</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>4</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>compact</td>
    </tr>
  </tbody>
</table>
</div>



```python
mpg.tail()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>229</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>19</td>
      <td>28</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>230</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>231</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>232</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>18</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>233</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>3.6</td>
      <td>2008</td>
      <td>6</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>17</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
  </tbody>
</table>
</div>



```python
mpg.shape
```

<pre>
(234, 11)
</pre>

```python
mpg.info()
```

<pre>
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 234 entries, 0 to 233
Data columns (total 11 columns):
 #   Column        Non-Null Count  Dtype  
---  ------        --------------  -----  
 0   manufacturer  234 non-null    object 
 1   model         234 non-null    object 
 2   displ         234 non-null    float64
 3   year          234 non-null    int64  
 4   cyl           234 non-null    int64  
 5   trans         234 non-null    object 
 6   drv           234 non-null    object 
 7   cty           234 non-null    int64  
 8   hwy           234 non-null    int64  
 9   fl            234 non-null    object 
 10  category      234 non-null    object 
dtypes: float64(1), int64(4), object(6)
memory usage: 20.2+ KB
</pre>

```python
mpg.describe()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>cty</th>
      <th>hwy</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>234.000000</td>
      <td>234.000000</td>
      <td>234.000000</td>
      <td>234.000000</td>
      <td>234.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>3.471795</td>
      <td>2003.500000</td>
      <td>5.888889</td>
      <td>16.858974</td>
      <td>23.440171</td>
    </tr>
    <tr>
      <th>std</th>
      <td>1.291959</td>
      <td>4.509646</td>
      <td>1.611534</td>
      <td>4.255946</td>
      <td>5.954643</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.600000</td>
      <td>1999.000000</td>
      <td>4.000000</td>
      <td>9.000000</td>
      <td>12.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>2.400000</td>
      <td>1999.000000</td>
      <td>4.000000</td>
      <td>14.000000</td>
      <td>18.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>3.300000</td>
      <td>2003.500000</td>
      <td>6.000000</td>
      <td>17.000000</td>
      <td>24.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>4.600000</td>
      <td>2008.000000</td>
      <td>8.000000</td>
      <td>19.000000</td>
      <td>27.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>7.000000</td>
      <td>2008.000000</td>
      <td>8.000000</td>
      <td>35.000000</td>
      <td>44.000000</td>
    </tr>
  </tbody>
</table>
</div>



```python
mpg.describe(include='object')
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>manufacturer</th>
      <th>model</th>
      <th>trans</th>
      <th>drv</th>
      <th>fl</th>
      <th>category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>234</td>
      <td>234</td>
      <td>234</td>
      <td>234</td>
      <td>234</td>
      <td>234</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>15</td>
      <td>38</td>
      <td>10</td>
      <td>3</td>
      <td>5</td>
      <td>7</td>
    </tr>
    <tr>
      <th>top</th>
      <td>dodge</td>
      <td>caravan 2wd</td>
      <td>auto(l4)</td>
      <td>f</td>
      <td>r</td>
      <td>suv</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>37</td>
      <td>11</td>
      <td>83</td>
      <td>106</td>
      <td>168</td>
      <td>62</td>
    </tr>
  </tbody>
</table>
</div>



```python
mpg.describe(include='all')
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>234</td>
      <td>234</td>
      <td>234.000000</td>
      <td>234.000000</td>
      <td>234.000000</td>
      <td>234</td>
      <td>234</td>
      <td>234.000000</td>
      <td>234.000000</td>
      <td>234</td>
      <td>234</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>15</td>
      <td>38</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>10</td>
      <td>3</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5</td>
      <td>7</td>
    </tr>
    <tr>
      <th>top</th>
      <td>dodge</td>
      <td>caravan 2wd</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>auto(l4)</td>
      <td>f</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>r</td>
      <td>suv</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>37</td>
      <td>11</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>83</td>
      <td>106</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>168</td>
      <td>62</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.471795</td>
      <td>2003.500000</td>
      <td>5.888889</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>16.858974</td>
      <td>23.440171</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>std</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.291959</td>
      <td>4.509646</td>
      <td>1.611534</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>4.255946</td>
      <td>5.954643</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>min</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.600000</td>
      <td>1999.000000</td>
      <td>4.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>9.000000</td>
      <td>12.000000</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.400000</td>
      <td>1999.000000</td>
      <td>4.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>14.000000</td>
      <td>18.000000</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.300000</td>
      <td>2003.500000</td>
      <td>6.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>17.000000</td>
      <td>24.000000</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>4.600000</td>
      <td>2008.000000</td>
      <td>8.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19.000000</td>
      <td>27.000000</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>max</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>7.000000</td>
      <td>2008.000000</td>
      <td>8.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>35.000000</td>
      <td>44.000000</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>


cf) 함수(내장함수, 패키지 함수), 메서드, 어트리뷰트 <br>

- 내장 함수 : 가장 기본적인 함수로 파이썬에 내장. 함수명 및 괄호 입력해서 사용. ex) sum(var)

- 패키지 함수 : 패키지를 로드해야 사용. 패키지명 뒤에 점 찍고 함수명 및 괄호 입력해서 사용. <br>

  ex) pd.DataFrame({'x':[1, 2, 3]})

- 메서드 : '변수가 지니고 있는 함수'. 변수명 뒤에 점 찍고 메서드명 및 괄호 입력해서 사용. <br>

  ex) df.head()  <br> 

  = 변수의 자료구조에 따라 사용할 수 있는 메서드가 다르다.

- 어트리뷰트 : '변수가 지니고 있는 값'. 변수명 뒤에 점 찍고 어트리뷰트명 입력해서 사용. 괄호 X <br>

  ex) df.shape ; df.index ; df.columns  <br> 

  = 이 역시 변수의 자료구조에 따라 사용할 수 있는 어트리뷰트가 다르다.


## 05-2. 변수명 바꾸기 (113-115쪽)

- 목적 : 변수명을 이해하기 쉬운 단어로 변경 -> 데이터를 수월하게 다룰 수 있음

- df.rename()



```python
df_raw = pd.DataFrame({'var1':[1, 2, 1],
                       'var2':[2, 3, 2],})
df_raw
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>var1</th>
      <th>var2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



```python
df_new = df_raw.copy()
df_new
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>var1</th>
      <th>var2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



```python
df_new = df_new.rename(columns = {'var2' : 'v2'}) # var2를 v2로 수정
df_new
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>var1</th>
      <th>v2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>


### [개인 실습] 혼자서 해보기(115쪽)

- mpg 데이터의 변수명은 긴 단어를 짧게 줄인 축약어로 되어 있다. cty는 도시 연비, hwy는 고속도로 연비를 의미한다. 변수명을 이해하기 쉬운 단어로 바꾸려 한다.


#### Q1 : mpg 데이터를 불러와 복사본을 만드세요.



```python
mpg_new = mpg.copy()
mpg_new
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>18</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>1</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>2</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>20</td>
      <td>31</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>3</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(av)</td>
      <td>f</td>
      <td>21</td>
      <td>30</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>4</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>229</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>19</td>
      <td>28</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>230</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>231</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>232</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>18</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>233</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>3.6</td>
      <td>2008</td>
      <td>6</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>17</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
  </tbody>
</table>
<p>234 rows × 11 columns</p>
</div>


#### Q2 : 복사본 데이터를 이용해 cty는 city로, hwy는 highway로 수정하세요



```python
mpg_new = mpg_new.rename(columns = {'cty' : 'city', 
                                    'hwy' : 'highway'})
mpg_new
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>city</th>
      <th>highway</th>
      <th>fl</th>
      <th>category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>18</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>1</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>2</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>20</td>
      <td>31</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>3</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(av)</td>
      <td>f</td>
      <td>21</td>
      <td>30</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>4</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>229</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>19</td>
      <td>28</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>230</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>231</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>232</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>18</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>233</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>3.6</td>
      <td>2008</td>
      <td>6</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>17</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
  </tbody>
</table>
<p>234 rows × 11 columns</p>
</div>


## 05-3. 파생변수 만들기 (116-128쪽)



```python
import pandas as pd

df = pd.DataFrame({'var1':[4, 3, 8], 
                   'var2':[2, 6, 1]})
df
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>var1</th>
      <th>var2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



```python
df['var_sum'] = df['var1'] + df['var2']
df
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>var1</th>
      <th>var2</th>
      <th>var_sum</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4</td>
      <td>2</td>
      <td>6</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>6</td>
      <td>9</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>1</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>



```python
df['var_mean'] = (df['var1'] + df['var2']) / 2
df
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>var1</th>
      <th>var2</th>
      <th>var_sum</th>
      <th>var_mean</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4</td>
      <td>2</td>
      <td>6</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>6</td>
      <td>9</td>
      <td>4.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>1</td>
      <td>9</td>
      <td>4.5</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 실습 : mpg 통합 연비 변수 만들기 (117쪽)

mpg = pd.read_csv('mpg.csv')
mpg
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>18</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>1</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>2</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>20</td>
      <td>31</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>3</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(av)</td>
      <td>f</td>
      <td>21</td>
      <td>30</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>4</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>229</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>19</td>
      <td>28</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>230</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>231</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>232</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>18</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>233</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>3.6</td>
      <td>2008</td>
      <td>6</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>17</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
  </tbody>
</table>
<p>234 rows × 11 columns</p>
</div>



```python
mpg['total'] = (mpg['cty'] + mpg['hwy']) / 2
mpg.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>category</th>
      <th>total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>18</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
      <td>23.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
      <td>25.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>20</td>
      <td>31</td>
      <td>p</td>
      <td>compact</td>
      <td>25.5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(av)</td>
      <td>f</td>
      <td>21</td>
      <td>30</td>
      <td>p</td>
      <td>compact</td>
      <td>25.5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>compact</td>
      <td>21.0</td>
    </tr>
  </tbody>
</table>
</div>



```python
sum(mpg['total']) / len(mpg['total'])
```

<pre>
20.14957264957265
</pre>

```python
mpg['total'].mean()
```

<pre>
20.14957264957265
</pre>

```python
# 조건물을 활용해 파생변수 만들기
## 1) 기준값 정하기

mpg['total'].describe()
```

<pre>
count    234.000000
mean      20.149573
std        5.050290
min       10.500000
25%       15.500000
50%       20.500000
75%       23.500000
max       39.500000
Name: total, dtype: float64
</pre>

```python
mpg['total'].plot.hist()
```

<pre>
<Axes: ylabel='Frequency'>
</pre>

<img src="data:image/png;base64,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aaedlmnTpmWvvfbaZJulS5fWlvv379/i8QcMGLDF/dpq4/0BAACAXUeXjTJ77LFHTj311LznPe/JkCFD0rt37zz77LOZPXt2brrppjz33HO5++6709jYmB/+8Id5wxveUNt31apVteXevXu3+Dkbv1L7xRdfbP9fBAAAAOiUumyUaWpqyt57773Zz0844YRMmDAho0ePzrx58zJ79uzceOON+ad/+qfaNmvXrq0td+/evcXP6dGjR215zZo12zzO1q6uWb58eY444ohtPi4AAABQVpeNMlsKMhvsv//+ueuuuzJ06NCsW7cukydP3iTK9OzZs7a8bt26Fj/n5Zdfri2//rXZbdHa7VEAAABA5+TtS1txyCGH5IQTTkjy2nNmnn766dq6Pffcs7bc2i1JL730Um25tVudAAAAgK5DlGnBsGHDassbXoGdbHr1SmtvR9r49iMP7QUAAAA2EGVaUK1Wt/jzjWPNggULWjzGxuuHDh3aPgMDAAAAOj1RpgUbvy67b9++teWDDz649v3s2bNbPMacOXOSJP369cvAgQPbf5AAAABApyTKbMWTTz6ZH/7wh0lee75Mv379ausqlUoaGxuTvHYlzKOPPrrFYzz66KO1K2UaGxtTqVQ6eNQAAABAZ9Elo8y9996b5ubmra7/05/+lA984AN55ZVXkiT/8A//sNk2F198cRoaXnt51YQJEzZ73fWaNWsyYcKEJElDQ0Muvvjidho9AAAAsCvokq/EnjBhQl555ZWcfvrpOeqoozJw4MDsvvvuWblyZR566KHcdNNNee6555Ikxx577BajzODBg3PppZdm4sSJmTt3bo455phcccUVGTRoUBYtWpRrr7028+bNS5JcdtllOfTQQ+v6OwIAAAA7ty4ZZZLk6aefzuTJkzN58uStbnP66afn5ptvTo8ePba4/gtf+EJWrFiRW265JfPmzcuZZ5652Tbjx4/PNddc027jBgAAAHYNXTLKfOMb38js2bPzyCOP5Mknn8zKlSvzwgsvpHfv3hkwYECOPvronHPOOTnqqKNaPE63bt0yderUnH766ZkyZUoef/zxrFy5Mn369MnIkSNz4YUXZvTo0XX6rQAAAIDOpEtGmVGjRmXUqFHtdryTTjopJ510UrsdDwAAANj1dckH/QIAAACUJsoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKvM7ll1+eSqVS+3rooYda3WfWrFkZO3Zs+vfvnx49eqR///4ZO3ZsZs2a1fEDBgAAADolUWYjv/rVrzJp0qQ2b1+tVnPhhRdm9OjRmTFjRpqamrJu3bo0NTVlxowZGT16dC688MJUq9UOHDUAAADQGYky/8/69etz/vnnp7m5Ofvtt1+b9rnqqqsyZcqUJMnw4cMzffr0PPbYY5k+fXqGDx+eJJkyZUo+/elPd9i4AQAAgM5JlPl//uM//iOPP/54hgwZkvHjx7e6/cKFC3PdddclSUaMGJGf/vSnOfPMMzNy5MiceeaZefjhhzNixIgkybXXXptFixZ16PgBAACAzkWUSbJ06dLa1Sw33nhjunfv3uo+kyZNSnNzc5Jk8uTJ2X333TdZv8cee2Ty5MlJkubm5lx//fXtO2gAAACgUxNlknziE5/Iiy++mHPOOSfHHXdcq9tXq9Xcc889SZIhQ4bkyCOP3OJ2Rx55ZA477LAkyd133+3ZMgAAAEBNl48yd955Z+6777686U1vyr/927+1aZ/FixenqakpSTJq1KgWt92wftmyZVmyZMkOjRUAAADYdXTpKPOXv/wlF110UZLXnvuy7777tmm/+fPn15aHDBnS4rYbr994PwAAAKBrayg9gJIuv/zyPPPMMzn66KPb9HDfDZYuXVpb7t+/f4vbDhgwYIv7tdWyZctaXL98+fJtPiYAAABQXpeNMg8//HBuvvnmNDQ05KabbkqlUmnzvqtWraot9+7du8Vte/XqVVt+8cUXt3mcG0cdAAAAYNfRJW9fWrduXS644IJUq9V88pOfzOGHH75N+69du7a23Nqbmnr06FFbXrNmzbYNFAAAANhldckrZb74xS9m/vz5efOb35zPfvaz27x/z549a8vr1q1rcduXX365tvz612a3RWu3PC1fvjxHHHHENh8XAAAAKKvLRZkFCxbkS1/6UpJk8uTJm9xe1FZ77rlnbbm1W5Jeeuml2nJrtzptSWvPrAEAAAA6py4XZSZNmpR169blkEMOyerVq3P77bdvts1vfvOb2vKPf/zjPPPMM0mS97///enVq9cmoaS1B/FufKWL58MAAAAAG3S5KLPhdqInn3wyZ511Vqvb/+u//mttefHixenVq1eGDRtW+9mCBQta3H/j9UOHDt3W4QIAAAC7qC75oN8ddfDBB6dv375JktmzZ7e47Zw5c5Ik/fr1y8CBAzt6aAAAAEAn0eWizLRp01KtVlv82vjhvw8++GDt5xuiSqVSSWNjY5LXroR59NFHt/hZjz76aO1KmcbGxm167TYAAACwa+tyUaa9XHzxxWloeO3urwkTJmz2uus1a9ZkwoQJSZKGhoZcfPHF9R4iAAAAsBMTZbbT4MGDc+mllyZJ5s6dm2OOOSZ33HFH5s6dmzvuuCPHHHNM5s6dmyS57LLLcuihh5YcLgAAALCT6XIP+m1PX/jCF7JixYrccsstmTdvXs4888zNthk/fnyuueaaAqMDAAAAdmaulNkB3bp1y9SpUzNz5sw0Njamb9++6d69e/r27ZvGxsZ873vfy80335xu3fxjBgAAADblSpktuPrqq3P11Ve3efuTTjopJ510UscNCAAAANjluIQDAAAAoABRBgAAAKAAUQYAAACgAFEGAAAAoABRBgAAAKAAUQYAAACgAFEGAAAAoABRBgAAAKAAUQYAAACgAFEGAAAAoABRBgAAAKAAUQYAAACgAFEGAAAAoABRBgAAAKAAUQYAAACgAFEGAAAAoABRBgAAAKAAUQYAAACgAFEGAAAAoABRBgAAAKAAUQYAAACgAFEGAAAAoABRBgAAAKAAUQYAAACgAFEGAAAAoABRBgAAAKAAUQYAAACgAFEGAAAAoABRBgAAAKAAUQYAAACgAFEGAAAAoABRBgAAAKAAUQYAAACgAFEGAAAAoABRBgAAAKAAUQYAAACgAFEGAAAAoICG0gMAAHY+A6+cWXoIXcKSiSeXHgIAUJArZQAAAAAKEGUAAAAAChBlAAAAAAoQZQAAAAAKEGUAAAAAChBlAAAAAAoQZQAAAAAKqHuU+bu/+7t8+9vfziuvvFLvjwYAAADYadQ9ytx///0588wzc+CBB+biiy/Or371q3oPAQAAAKC4ukeZ/fbbL9VqNX/+858zefLk/O3f/m3e/va354Ybbshf/vKXeg8HAAAAoIi6R5mmpqbcc889Oe2009LQ0JBqtZp58+ZlwoQJ6du3bz784Q/ngQceqPewAAAAAOqq7lFmt912y/vf//5897vfzbJly/LlL385b33rW1OtVrN27drcfvvted/73peDDz44n//85/PUU0/Ve4gAAAAAHa7o25f23XfffOpTn8qvf/3rPP744/nYxz6WvffeO9VqNX/84x/zuc99LoccckhOOOGE3HHHHVm3bl3J4QIAAAC0m53mldgbnivz9NNP5z//8z/z3ve+N5VKJevXr8+Pf/zjfOhDH8qBBx6YCRMmZN68eaWHCwAAALBDdpoos0GPHj1y5pln5v77788DDzyQAw44oLbu+eefzw033JARI0bkHe94R+6+++5yAwUAAADYATtdlFm9enVuu+22HH/88XnPe96TP/3pT6lWq6lWqxk2bFh23333VKvVPP744zn99NPT2NiYtWvXlh42AAAAwDbZaaLMT3/605x33nk58MADc+6552b27NmpVqt54xvfmI997GOZO3dufvOb3+SZZ57J1772tQwdOjTVajX33XdfJk6cWHr4AAAAANukaJRpamrKl770pRx22GF517velVtvvTWrVq1KtVrNMccck2nTpuXpp5/ODTfckL/9279NkvTu3Tvnn39+nnjiifz93/99qtVq/vM//7PkrwEAAACwzRrq/YHr1q3L3XffnVtvvTUPPPBA1q9fn2q1muS1tzGdffbZOe+883LYYYe1eJxu3brlk5/8ZO6444788Y9/rMfQAQAAANpN3aPMgQcemL/85S9Jkmq1mm7duuWEE07Ieeedl8bGxrzhDW9o87H+5m/+JknS3NzcEUMFAAAA6DB1jzLPP/98kmTAgAE599xz89GPfjRvfvObt+tYb3rTm/LZz362PYcHAAAAUBd1jzJjxozJeeedl7/7u79LpVLZoWPts88+ogwAAADQKdU9ynznO9+p90cCAAAA7HR2mldiAwAAAHQldb9SZtWqVZk0aVKS5IILLsgBBxzQ4vbLly/P17/+9STJZZddlt13373DxwgAAADQ0ep+pczdd9+dq6++Ot/61rdaDTJJcsABB+Rb3/pWPve5z+Xee++twwgBAAAAOl7do8x3v/vdVCqVnHHGGW3avlKp5Mwzz0y1Ws23v/3tDh4dAAAAQH3UPcosWLAgSXL00Ue3eZ+jjjoqSfK73/2uQ8YEAAAAUG91jzLLli1Lkhx44IFt3mfDbU5NTU0dMiYAAACAeqt7lOnW7bWPXL16dZv32bBtc3Nzh4wJAAAAoN7qHmU2XCEzd+7cNu+zYdu2PBgYAAAAoDOoe5R55zvfmWq1mhtuuCGvvPJKq9u/8sorueGGG1KpVHLsscfWYYQAAAAAHa/uUebcc89NkvzhD3/Ihz70oRZvY1q9enXOOuus/P73v99kXwAAAIDOrqHeH3j00UfnzDPPzO23357vfve7+dnPfpbzzz8/73rXu3LggQemUqnk6aefzpw5c3LzzTdn2bJlqVQq+cAHPpBRo0bVe7gAAAAAHaLuUSZJbrnllqxcuTIPPPBAmpqacvXVV29xu2q1miQ54YQT8o1vfKOOIwQAAADoWHW/fSlJevbsmR/84AeZNGlS+vbtm2q1usWvAQMG5D/+4z8ya9as9OzZs8RQAQAAADpEkStlkqRSqeSiiy7KP/3TP+WXv/xl5s2bl5UrVyZJ+vTpk7/927/N//gf/yOVSqXUEAEAAAA6TLEos0GlUsnw4cMzfPjw0kMBAAAAqJsity8BAAAAdHWiDAAAAEABRW9f+tWvfpWf/OQnefLJJ7Nq1aq8+uqrLW5fqVQyderUOo0OAAAAoOMUiTL/9V//lY9+9KN59NFH27xPtVoVZQAAAIBdRt2jTFNTU971rndl5cqVqVarSZLevXtnn332Sbdu7qYCAAAAuoa6R5kvfOELefbZZ1OpVHLeeefl0ksvzeDBg+s9DAAAAICi6h5lZs2alUqlkrPPPjtTpkyp98cDAAAA7BTqfr/Q008/nSQ5++yz6/3RAAAAADuNukeZffbZJ0my99571/ujAQAAAHYadY8yI0aMSJL8/ve/r/dHAwAAAOw06h5l/umf/inVatXzZAAAAIAure5R5oQTTsjll1+eBx98MB//+Mfzyiuv1HsIAAAAAMXV/e1Lt912W4YNG5ajjz46U6ZMyb333psPfOADGTJkSPbYY49W9/eAYAAAAGBXUPcoM27cuFQqldr3y5cvz+TJk9u074ZXaQMAAAB0dnWPMklSrVZLfCwAAADATqPuUWbx4sX1/kgAAACAnU7do8xBBx1U748EAAAA2OnU/e1LAAAAAIgyAAAAAEUUedDvBgsXLsxtt92WRx55JM8880zWrFmTWbNm5S1veUttm9/85jd56qmn0qtXr4waNargaAEAAADaT5Eos379+lxxxRW5/vrrs379+trbmCqVStatW7fJtkuXLs0pp5yShoaGLF68OP369SsxZAAAAIB2VeT2pQsvvDBf/epX8+qrr6Zv3775wAc+sNVtR48enUMOOSSvvvpq7rrrrjqOEgAAAKDj1D3KPPTQQ5k6dWqS5F/+5V+yZMmS3HnnnS3u88EPfjDVajUPPvhgPYYIAAAA0OHqfvvSTTfdlCQ56aSTcs0117RpnyOOOCJJ8tvf/rbDxgUAAABQT3W/UuaRRx5JpVLJ+PHj27xP//79kyTPPPNMRw0LAAAAoK7qHmVWrFiRJDn44IPbvE9Dw2sX9LzyyisdMiYAAACAeqt7lNl9992TJKtXr27zPk899VSSZJ999mmXMbzwwgu5/fbbc8kll2TUqFF5y1vekr322ivdu3fPfvvtl+OOOy7XXXddnnvuuTYdb9asWRk7dmz69++fHj16pH///hk7dmxmzZrVLuMFAAAAdj11jzIbrpCZN29em/e57777kiTDhg1rlzE89thjOeuss/LVr341c+bMyaJFi/LCCy/klVdeybPPPpvZs2fniiuuyJAhQ/KDH/xgq8epVqu58MILM3r06MyYMSNNTU1Zt25dmpqaMmPGjIwePToXXnhh7ZXfAAAAABvUPcqceOKJqVarmTJlStavX9/q9j//+c/zzW9+M5VKJX/3d3/XbuMYMGBAzj777Pz7v/97vvvd7+aRRx7JT3/609xxxx354Ac/mN122y0rV67Mqaeeml//+tdbPMZVV12VKVOmJEmGDx+e6dOn57HHHsv06dMzfPjwJMmUKVPy6U9/ut3GDQAAAOwaKtU6X8bR1NSUwYMHZ+3atRk3blxuuummvOENb0i3bt1SqVTyxBNP1K6I+c53vpOPfexjee6557LXXntlyZIl2WuvvXZ4DK+++mp22223Fre5++67M2bMmCTJ2LFj853vfGeT9QsXLszQoUPT3NycESNGZM6cObVbs5LXbs8aNWpU5s6dm4aGhixYsCCDBg3a4bG/3rJlyzJgwIAkydKlS2sPRYYNBl45s/QQuoQlE08uPYQuwfnMrsbcAQCdR0f8/V33K2X69euX//iP/0i1Ws20adNyyCGH5BOf+ERt/dSpU/Pxj388hx56aM4444w899xzqVQqmTJlSrsEmSStBpkkOe200zJkyJAkyZw5czZbP2nSpDQ3NydJJk+evEmQSZI99tgjkydPTpI0Nzfn+uuv38FRAwAAALuSukeZJBk/fnxuvvnm7L777mlqasrXvva1VCqVJMn111+fKVOmZNGiRalWq+nRo0duueWWfPCDH6z7OHv16pUkWbt27SY/r1arueeee5IkQ4YMyZFHHrnF/Y888sgcdthhSV678sazZQAAAIANikSZJPnoRz+aBQsW5FOf+lQGDRqUarW6yVe/fv3y8Y9/PPPnz88555xT9/HNnz8/v/zlL5OkdsXMBosXL05TU1OSZNSoUS0eZ8P6ZcuWZcmSJe0+TgAAAKBzaij54f3798+Xv/zlfPnLX84LL7yQFStW5NVXX83f/M3fpE+fPnUfz+rVq9PU1JR777031113XV599dUkyUUXXbTJdvPnz68tvz7YvN7G6+fPn197+1RbLVu2rMX1y5cv36bjAQAAADuHolFmY2984xvzxje+se6fO23atJx77rlbXX/ppZfmwx/+8CY/W7p0aW25tQf7bHgI0Ov3a6uN9wcAAAB2HTtNlNnZvO1tb8tNN92Ud7zjHZutW7VqVW25d+/eLR5nw3NpkuTFF19svwECOxVvBQIAALZVl48yp512WkaMGJEkWbNmTRYtWpQ777wzM2bMyIc//OFcf/31OeWUUzbZZ+MH/3bv3r3F4/fo0aO2vGbNmm0eX2tX1yxfvjxHHHHENh8XAAAAKKvuUebd7373du9bqVTyox/9qB1Hk+y9997Ze++9a9+PHDkyZ555Zr75zW/mnHPOSWNjY6ZOnZpx48bVtunZs2dted26dS0e/+WXX64tv/612W3RHu89BwAAAHY+dY8yDz30UCqVSouvh97weuwNNmz7+p93pI985CO57777cuedd+Yf//Ef09jYmH322SdJsueee9a2a+2WpJdeeqm23NqtTgAAAEDXUfco8653vavVuPLSSy/lD3/4Q/7617+mUqlk8ODBOfDAA+s0wv9fY2Nj7rzzzrz00kv5/ve/nw996ENJNr16pbW3I218+5GH9gIAAAAbFLlSpi2q1WpmzpyZiy66KH/+859z880359hjj+3Ywb3OvvvuW1v+4x//WFseNmxYbXnBggUtHmPj9UOHDm3H0QEAAACdWbfSA9iaSqWSU045JQ8//HB22223jBkzJk1NTXUdw8aft/GtRwcffHD69u2bJJk9e3aLx5gzZ06SpF+/fhk4cGD7DxIAAADolHbaKLPBgQcemE996lN57rnnct1119X1s7/97W/Xlg8//PDacqVSSWNjY5LXroR59NFHt7j/o48+WrtSprGxsa7PxAEAAAB2bjt9lElSu21p5syZ7XK8adOmbfJa6y2ZNGlSvve97yVJBg4cuNmtUxdffHEaGl67+2vChAmbve56zZo1mTBhQpKkoaEhF198cbuMHQAAANg11P2ZMtuje/fuSZKnn366XY539dVX55JLLsnpp5+eY489NoMGDUrv3r2zatWqPPHEE/nWt76Vn/70p7XP/vrXv14LMBsMHjw4l156aSZOnJi5c+fmmGOOyRVXXJFBgwZl0aJFufbaazNv3rwkyWWXXZZDDz20XcYOAAAA7Bo6RZR5+OGHkyR77LFHux3zz3/+c77+9a/n61//+la36d+/f2655Za8973v3eL6L3zhC1mxYkVuueWWzJs3L2eeeeZm24wfPz7XXHNNu40bAAAA2DXs9FHmkUceyec///lUKpUcccQR7XLMH/3oR3nggQfy4IMPZv78+fnTn/6U5557Lj179sz++++ft73tbTnllFNyxhlntBiCunXrlqlTp+b000/PlClT8vjjj2flypXp06dPRo4cmQsvvDCjR49ulzEDAAAAu5ZKtVqt1vMDP//5z7e6zfr16/P8889n7ty5+dnPfpb169enUqlk1qxZOeGEE+owys5j2bJlGTBgQJJk6dKl6d+/f+ERsbMZeGX7PIsJADqrJRNPLj0EAHYBHfH3d92vlLn66qu36S1E1Wo1DQ0Nue666wQZAAAAYJdR5Pal1i7OqVQq2XPPPXPwwQdn1KhRueCCCzJs2LA6jQ4AAACg49U9yqxfv77eHwkAAACw0+lWegAAAAAAXZEoAwAAAFCAKAMAAABQQN2fKfPUU091yHHf/OY3d8hxAQAAADpC3aPMwQcf3O7HrFQqaW5ubvfjAgAAAHSUukeZ1l6HDQAAANAV1D3K3HrrrUmSG264IY8//nje8IY35MQTT8wRRxyR/fffP9VqNStWrMjjjz+e+++/P6+88kpGjhyZj3/84/UeKgAAAECHqXuUOeecc3Leeedl7ty5OfHEEzN16tT069dvi9s2NTXl/PPPzw9+8IMcfvjh+frXv17n0QIAAAB0jLq/femuu+7KLbfckhEjRmTmzJlbDTJJ0q9fv9x77715+9vfnltuuSV33nlnHUcKAAAA0HHqHmW+9rWvpVKp5FOf+lR22223Vrffbbfdcskll6RarWbKlCl1GCEAAABAx6t7lPn1r3+dJBk8eHCb99mw7RNPPNEhYwIAAACot7pHmVWrViVJVqxY0eZ9Nmy7YV8AAACAzq7uUeaggw5Kktx2221t3mfDtm9+85s7ZEwAAAAA9Vb3KNPY2JhqtZrbb7891113Xavbf/nLX8706dNTqVQyZsyYOowQAAAAoOPV/ZXYV155ZW677bb86U9/yj//8z9n+vTpOeecczJy5Mjst99+qVQq+dOf/pTHH3883/zmN/PLX/4ySXLAAQfkiiuuqPdwAQAAADpE3aPM3nvvnQceeCDve9/70tTUlF//+te55JJLtrp9tVpN//79M2vWrOy99971GygAAABAB6r77UtJMmzYsPz2t7/NJz/5yey9996pVqtb/Np7773zqU99Kr/5zW8ybNiwEkMFAAAA6BB1v1Jmgze+8Y35yle+ki996Uv5+c9/nieeeCLPP/98qtVq3vSmN+Xwww/P29/+9nTv3r3UEAEAAAA6TLEos0H37t1z1FFH5aijjio9FAAAAIC6KXL7EgAAAEBXV/xKmSeffDKPPPJInnnmmaxevTof//jH06dPn9LDAgAAAOhQxaLMvHnzcvHFF+fhhx/e5Oenn376JlHmf//v/53Pfe5z2WuvvfK73/0ub3jDG+o9VAAAAIB2V+T2pZkzZ+boo4/Oww8/vMnblrbknHPOyZo1a/Lkk0/mvvvuq/NIAQAAADpG3aPMM888k7POOisvv/xyhg0blu9///tZtWrVVrfv3bt3TjvttCTJ97///TqNEgAAAKBj1T3KTJo0KS+++GIOOuig/OQnP8n73ve+9OrVq8V9jjvuuFSr1fz85z+v0ygBAAAAOlbdo8wPfvCDVCqVXHLJJdl7773btM9hhx2WJFmyZEnHDQwAAACgjuoeZRYvXpwkOeKII9q8z5577pkkefHFFztkTAAAAAD1Vvco88orryTJNr1F6S9/+UuStHqbEwAAAEBnUfcoc8ABByT5/6+YaYtHHnkkSdK/f/8OGRMAAABAvdU9yhxzzDFJkhkzZrRp+9WrV+emm25KpVLJu971ro4cGgAAAEDd1D3KnHPOOalWq5k+fXruv//+Frd98cUXc8YZZ+Spp55KkowfP74eQwQAAADocHWPMu9973tz2mmnZf369Tn11FNz2WWX5bHHHqut//Of/5yf/exn+dd//dccdthh+f73v59KpZKzzz47w4cPr/dwAQAAADpEpVqtVuv9oatXr84pp5yShx56KJVKZavbbRjae97zntx3333p0aNHvYbYaSxbtiwDBgxIkixdutRzd9jMwCtnlh4CABS1ZOLJpYcAwC6gI/7+rvuVMkmyxx575IEHHsi//du/5YADDki1Wt3i15ve9KZ88YtfzA9+8ANBBgAAANilNJT64G7duuWSSy7JRRddlMceeyxz587NihUr8uqrr+Zv/uZvMnz48Bx77LFiDAAAALBLqnuUue2225Ikhx12WN7xjnekoaEhRx99dI4++uh6DwUAAACgmLrfvjRu3Lice+65+eMf/1jvjwYAAADYadQ9yuy1115JkkMPPbTeHw0AAACw06h7lDn44IOTJM8//3y9PxoAAABgp1H3KDNmzJhUq9Xce++99f5oAAAAgJ1G3aPMRRddlIMOOig33nhjfvzjH9f74wEAAAB2CnWPMm984xvzwx/+MEOGDMn73ve+XHDBBXnooYfy5z//OdVqtd7DAQAAACii7q/E3m233WrL1Wo1U6dOzdSpU9u0b6VSSXNzc0cNDQAAAKBu6h5lXn81jKtjAAAAgK6o7lHms5/9bL0/EgAAAGCn06FR5rbbbkuSnHbaaXnjG9+YRJQBAAAASDo4yowbNy6VSiUjRozIsGHDNlv/7LPP5sYbb0ylUsmnP/3pjhwKAAAAwE6l7rcvbWzFihW5+uqrRRkAAACgy6n7K7EBAAAAEGUAAAAAihBlAAAAAAoQZQAAAAAKEGUAAAAAChBlAAAAAAqoyyuxb7jhhuy3336b/XzFihW15c9//vNtOtZnPvOZdhsXAAAAQCl1iTI33njjVtdVKpUkyec+97k2HUuUAQAAAHYFHR5lqtVqux1rQ8ABAAAA6Ow6NMo8+OCDHXl4AAAAgE6rQ6PMqFGjOvLwAAAAAJ2Wty8BAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAUIMoAAAAAFCDKAAAAABQgygAAAAAU0GWjzC9+8Yt88YtfzOjRozNgwID06NEjvXv3zuDBgzNu3Lj85Cc/2abjzZo1K2PHjk3//v3To0eP9O/fP2PHjs2sWbM66DcAAAAAOrOG0gMoYdSoUZkzZ85mP1+3bl3+8Ic/5A9/+EO+8Y1v5CMf+UhuvvnmdO/efavHqlar+djHPpYpU6Zs8vOmpqbMmDEjM2bMyAUXXJCbbroplUql3X8XAAAAoHPqklfKNDU1JUn69u2biy66KHfddVcee+yxPPLII/nqV7+afv36JUm++c1vZty4cS0e66qrrqoFmeHDh2f69Ol57LHHMn369AwfPjxJMmXKlHz605/uuF8IAAAA6HQq1Wq1WnoQ9XbKKafk7LPPzumnn57ddttts/UrV67MMccck9///vdJkjlz5uSd73znZtstXLgwQ4cOTXNzc0aMGJE5c+Zk9913r61fvXp1Ro0alblz56ahoSELFizIoEGD2vV3WbZsWQYMGJAkWbp0afr379+ux6fzG3jlzNJDAICilkw8ufQQANgFdMTf313ySpn77rsvZ5xxxhaDTJL06dMnX/nKV2rf33XXXVvcbtKkSWlubk6STJ48eZMgkyR77LFHJk+enCRpbm7O9ddf3w6jBwAAAHYFXTLKtMVxxx1XW160aNFm66vVau65554kyZAhQ3LkkUdu8ThHHnlkDjvssCTJ3XffnS54YRIAAACwBaLMVqxbt6623K3b5v+YFi9eXHs2zahRo1o81ob1y5Yty5IlS9pvkAAAAECnJcpsxezZs2vLQ4YM2Wz9/PnzW1y/sY3Xb7wfAAAA0HV1yVdit2b9+vWZOHFi7fszzjhjs22WLl1aW27t4T4bHgT0+v3aYtmyZS2uX758+TYdDwAAANg5iDJbMGnSpDz22GNJkjFjxmTEiBGbbbNq1aracu/evVs8Xq9evWrLL7744jaNZeOgAwAAAOw63L70OrNnz86VV16ZJNlvv/1y4403bnG7tWvX1pa7d+/e4jF79OhRW16zZk07jBIAAADo7Fwps5Hf/va3GTNmTJqbm9OjR4/ceeed2X///be4bc+ePWvLGz8UeEtefvnl2vLrX5vdmtZud1q+fHmOOOKIbTomAAAAUJ4o8/8sXrw4J554Yp5//vnstttumT59eotvVdpzzz1ry63dkvTSSy/Vllu71en1WnteDQAAANA5uX0pydNPP533vve9efrpp1OpVHLLLbdkzJgxLe6zcSxp7WG8G1/t4hkxAAAAQCLKZOXKlTnhhBPy5JNPJkkmT56cs88+u9X9hg0bVltesGBBi9tuvH7o0KHbOVIAAABgV9Klo8xf//rXvO9978vvfve7JMnEiRPzD//wD23a9+CDD07fvn2TvPZw4JbMmTMnSdKvX78MHDhw+wcMAAAA7DK6bJRZvXp1Tj755PziF79Ikvyv//W/csUVV7R5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m/Of//mfWz2WuY2WtOe5toG5jZYMGDAgxx9/fN7+9rdnwIABOfDAA7N+/fosW7Ysd911V7773e9m5cqVOfXUU/P444/nv//3/77ZMcxrtEV7nGsbmNfYVuvXr8/555+f5ubm7LffflmxYkWr+3Taua10FaK8z3zmM9V77723+swzz1Sr1Wp18eLF23z1wh/+8IdaxRwxYkR19erVm6x/6aWXqiNGjKgmqTY0NFQXLlzY3r8GnUB7nGsb/1eXxYsXd9xg6dROPvnk6h133FFtbm7e4vpnn322Onjw4Nq5NGfOnC1uZ26jNe11rpnbaIutnWcbmzFjRu1cGjt27GbrzWu0RXuca+Y1dsSkSZOqSapDhgyp/vM//3OrV8p05rnNM2XI5z73uZxyyinZf//9t/sYkyZNSnNzc5Jk8uTJ2X333TdZv8cee2Ty5MlJkubm5lx//fXb/Vl0Xu1xrkFb3HfffTnjjDOy2267bXF9nz598pWvfKX2/V133bXF7cxttKa9zjVoi62dZxs77bTTMmTIkCTJnDlzNltvXqMt2uNcg+21dOnSfPrTn06S3HjjjenevXur+3TmuU2UYYdVq9Xcc889SZIhQ4bkyCOP3OJ2Rx55ZA477LAkyd13351qtVq3MQK83nHHHVdbXrRo0WbrzW20l9bONWhvvXr1SpKsXbt2k5+b12hvWzvXYEd84hOfyIsvvphzzjlnk/8P3ZrOPreJMuywxYsX1+6pHzVqVIvbbli/bNmyLFmypKOHBrBV69atqy1367b5/x2a22gvrZ1r0J7mz5+fX/7yl0lSu4phA/Ma7amlcw2215133pn77rsvb3rTm/Jv//Zvbdqns89t/s2AHTZ//vzacmsT8sbrN94Ptse4ceOy//77p3v37unTp0+OPPLIXHXVVbVJGVoye/bs2vKW5i5zG+2ltXPt9cxtbKvVq1fnD3/4Q7761a/m+OOPz6uvvpokueiiizbZzrzGjmrrufZ65jXa4i9/+UvtXLr22muz7777tmm/zj63efsSO2zp0qW15daenD5gwIAt7gfbY+M/dJ577rk899xz+dnPfpavfOUruf7663PhhRcWHB07s/Xr12fixIm1788444zNtjG30R7acq69nrmNtpg2bVrOPffcra6/9NJL8+EPf3iTn5nX2B7bc669nnmNtrj88svzzDPP5Oijj8748ePbvF9nn9tEGXbYqlWrasu9e/ducdsN950myYsvvthhY2LXdsghh2Ts2LE56qijahPrk08+me985zu56667snbt2nzsYx9LpVLJBRdcUHi07IwmTZqUxx57LEkyZsyYjBgxYrNtzG20h7acaxuY22gPb3vb23LTTTflHe94x2brzGu0p5bOtQ3Ma7TVww8/nJtvvjkNDQ256aabUqlU2rxvZ5/bRBl22MYP9mrtydg9evSoLa9Zs6bDxsSua8yYMTnnnHM2m6hHjhyZv//7v899992XsWPH5pVXXsknP/nJnHrqqTnggAMKjZad0ezZs3PllVcmSfbbb7/ceOONW9zO3MaOauu5lpjb2HannXZaLfKtWbMmixYtyp133pkZM2bkwx/+cK6//vqccsopm+xjXmN7bM+5lpjXaLt169blggsuSLVazSc/+ckcfvjh27R/Z5/bPFOGHdazZ8/a8sYPM9ySl19+ubb8+teUQVvstddeLZbzU045JZ/97GeTvHbf89SpU+s1NDqB3/72txkzZkyam5vTo0eP3HnnnVt9Rbu5jR2xLedaYm5j2+29995561vfmre+9a0ZOXJkzjzzzHz3u9/NbbfdlieffDKNjY2ZNm3aJvuY19ge23OuJeY12u6LX/xi5s+fnze/+c21c2JbdPa5TZRhh+2555615dYuAXvppZdqy61dWgbb6/zzz6/9S8DG9zDTtS1evDgnnnhinn/++ey2226ZPn16i0/oN7exvbb1XGsrcxtt8ZGPfCQf/OAHs379+vzjP/5jnn/++do68xrtqaVzra3MayxYsCBf+tKXkiSTJ0/e5Paitursc5vbl9hhGz9MadmyZS1uu/HDlDZ+yBK0p/322y99+vTJs88+66n+JEmefvrpvPe9783TTz+dSqWSW265JWPGjGlxH3Mb22N7zrW2MrfRVo2Njbnzzjvz0ksv5fvf/34+9KEPJTGv0f62dq61lXmNSZMmZd26dTnkkEOyevXq3H777Ztt85vf/Ka2/OMf/zjPPPNMkuT9739/evXq1ennNlGGHTZs2LDa8oIFC1rcduP1Q4cO7bAxQbVaLT0EdhIrV67MCSeckCeffDLJa/8V5uyzz251P3Mb22p7z7VtYW6jLTZ+jewf//jH2rJ5jfa2tXNtW5jXurYNtxM9+eSTOeuss1rd/l//9V9ry4sXL06vXr06/dzm9iV22MEHH5y+ffsmaf2ywzlz5iRJ+vXrl4EDB3b00OiiVqxYkeeeey5JaucmXdNf//rXvO9978vvfve7JMnEiRPzD//wD23a19zGttiRc62tzG201cZXHGx8eb55jfa2tXOtrcxrtIfOPreJMuywSqWSxsbGJK+Vx0cffXSL2z366KO1MtnY2LhNrzmDbTFlypTaf3Vpj+c40DmtXr06J598cn7xi18kSf7X//pfueKKK9q8v7mNttrRc62tzG201be//e3a8sZvMTGv0d62dq61lXmNadOmpVqttvi18cN/H3zwwdrPN0SVTj+3VeF1Fi9eXE1STVI955xz2rTPf/3Xf1UbGhqqSaojRoyorl69epP1q1evro4YMaKapNrQ0FD9/e9/3wEjp7PZ1nNt8eLF1V/84hctbnPvvfdWu3fvXk1S7dmzZ3XZsmXtNFo6k5dffrl64okn1s6viy66aLuOY26jNe1xrpnbaKtbb721umbNmha3+epXv1o7HwcOHFh95ZVXNllvXqMtdvRcM6/Rnj772c/WzrUHH3xwi9t05rnNM2XIww8/nIULF9a+X7lyZW154cKFm73ibty4cZsdY/Dgwbn00kszceLEzJ07N8ccc0yuuOKKDBo0KIsWLcq1116befPmJUkuu+yyHHrooR3yu7Bz29FzbcmSJTn++ONz1FFH5f3vf3/e9ra3Zb/99ku1Ws2TTz6Zu+66K3fddVftv7h8+ctfTr9+/Trs92HnddZZZ+X+++9Pkrz73e/O+PHjN3lI3Ot17949gwcP3uzn5jZa0x7nmrmNtrr66qtzySWX5PTTT8+xxx6bQYMGpXfv3lm1alWeeOKJfOtb38pPf/rTJK+da1//+tfT0LDpv+6b12iLHT3XzGvUW6ee20oWIXYO55xzTq08tuVra1599dXqRz/60Rb3HT9+fPXVV1+t42/HzmRHz7UHH3ywTfvtscce1a997WsFfkN2FttyniWpHnTQQVs9lrmNlrTHuWZuo60OOuigNp0r/fv3r95///1bPY55jdbs6LlmXqM9teVKmWq1885trpSh3XTr1i1Tp07N6aefnilTpuTxxx/PypUr06dPn4wcOTIXXnhhRo8eXXqYdGJvf/vb83/+z//JI488krlz52b58uVZuXJlmpubs88+++S//bf/lve85z0577zzst9++5UeLrsIcxsdzdxGW/3oRz/KAw88kAcffDDz58/Pn/70pzz33HPp2bNn9t9//7ztbW/LKaeckjPOOCN77LHHVo9jXqM1O3qumdcoobPObZVq1TvIAAAAAOrN25cAAAAAChBlAAAAAAoQZQAAAAAKEGUAAAAAChBlAAAAAAoQZQAAAAAKEGUAAAAAChBlAAAAAAoQZQAAAAAKEGUAAAAAChBlAAAAAAoQZQAAAAAKEGUAAAAAChBlAAAAAAoQZQAAAAAKEGUAAAAAChBlAAAAAAoQZQAAAAAKEGUAAAAAChBlAAAAAAoQZQAAAAAKEGUAAAAAChBlAAAAAAoQZQAAAAAK+P8AuIF+J3Qa6C4AAAAASUVORK5CYII="/>


```python
## 2. 합격 판정 변수 만들기

import numpy as np
```


```python
mpg['test'] = np.where(mpg['total'] >= 20, 'pass', 'fail')
mpg.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>category</th>
      <th>total</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>18</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
      <td>23.5</td>
      <td>pass</td>
    </tr>
    <tr>
      <th>1</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
      <td>25.0</td>
      <td>pass</td>
    </tr>
    <tr>
      <th>2</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>20</td>
      <td>31</td>
      <td>p</td>
      <td>compact</td>
      <td>25.5</td>
      <td>pass</td>
    </tr>
    <tr>
      <th>3</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(av)</td>
      <td>f</td>
      <td>21</td>
      <td>30</td>
      <td>p</td>
      <td>compact</td>
      <td>25.5</td>
      <td>pass</td>
    </tr>
    <tr>
      <th>4</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>compact</td>
      <td>21.0</td>
      <td>pass</td>
    </tr>
  </tbody>
</table>
</div>



```python
## 3. 빈도표로 합격 판정 자동차 수 살펴보기

mpg['test'].value_counts()
```

<pre>
test
pass    128
fail    106
Name: count, dtype: int64
</pre>

```python
## 4. 막대 그래프로 빈도 표현하기

count_test = mpg['test'].value_counts()
count_test.plot.bar()
```

<pre>
<Axes: xlabel='test'>
</pre>
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABFAAAAOFCAYAAABN0xYuAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjcuMiwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8pXeV/AAAACXBIWXMAAB7CAAAewgFu0HU+AABPVElEQVR4nO3de7iXZYHv/88XkIOgIokHhAJNBC0nFAgHDe1gIzKSTBlO5SFTq5GiyUO7n5nu8XxIG2bSzQaj9hRZGjiKUqkImBBiJmmggmCAGFIekKMLv78/uPgOCHKDclhr8XpdF9f1rOe5n3vdX/5wud48h0q1Wq0GAAAAgLfVZGcvAAAAAKC+E1AAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoaLazF7CrWLlyZf74xz8mSdq3b59mzfzVAwAAwLZWV1eXl156KUnywQ9+MC1bttwm8/otfgf54x//mN69e+/sZQAAAMAuY9q0aenVq9c2mcstPAAAAAAFrkDZQdq3b1/bnjZtWg444ICduBoAAABonBYtWlS7A2T938XfLQFlB1n/mScHHHBAOnbsuBNXAwAAAI3ftnz+qFt4AAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKGi2sxcAjVnnb43b2UsAtpN515y0s5cAAMAO5AoUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgILtGlAWL16ce+65J5deemlOPPHE7LPPPqlUKqlUKjnzzDO3aI6VK1fmrrvuypAhQ/LhD3847dq1y2677ZZ27drl6KOPzmWXXZZFixZt8ZqWL1+e66+/Pr179067du3Spk2bdO/ePRdccEH+/Oc/v8NPCgAAADRmzbbn5Pvtt9+7On/GjBk55phjsnTp0o2Ovfzyy5k6dWqmTp2a733vexkxYkROPfXUzc43Z86cnHTSSXn66ac32D9r1qzMmjUrI0aMyE9/+tP079//Xa0bAAAAaFx22C08nTp1ygknnLBV57z22mu1eNK3b99cffXV+c1vfpPf//73+dWvfpXzzjsvTZs2zdKlS/PP//zPue+++952rtdffz0DBgyoxZNzzjknDzzwQB555JFceeWVadOmTV599dV85jOfyYwZM975BwUAAAAane16Bcqll16aXr16pVevXtlvv/0yb968dOnSZYvPb9KkSU499dR897vfzWGHHbbR8RNOOCEnnnhiTjnllKxZsyZDhgzJs88+m0qlstHYG264IbNmzUqSXHfddbnwwgtrx44++ugcf/zx+chHPpLly5dn6NChefDBB9/BJwYAAAAao+16Bcrll1+eAQMGvONbef7+7/8+t99++ybjyToDBw7MoEGDkqy9RecPf/jDRmPeeOONfP/730+SdO/ePd/85jc3GnP00Ufn7LPPTpJMmDAhjz322DtaMwAAAND4NIq38Bx//PG17Tlz5mx0/KGHHsorr7ySJDnjjDPSpMmmP/b6D7b95S9/uU3XCAAAADRcjSKgrFq1qra9qTgyefLk2na/fv3edp6ePXumdevWSZKHH354G64QAAAAaMgaRUCZOHFibbtbt24bHZ85c+Zmj6/TrFmzHHzwwRudAwAAAOzatutDZHeEJ554IuPGjUuSHH744Zt8Xsr8+fOTJK1bt07btm03O1+nTp0yY8aMvPTSS1m1alVatGixRetYsGDBZo8vWrRoi+YBAAAA6p8GHVBWrVqVL33pS1mzZk2S5KqrrtrkuHWvQm7Tpk1xznW38CRrX328pQGlU6dOWzQOAAAAaHga9C08559/fqZPn55k7cNhTz755E2OW7lyZZKkefPmxTnXDyYrVqzYBqsEAAAAGroGewXK1VdfnREjRiRJjjrqqPznf/7n245t2bJlkmT16tXFedd/IG2rVq22eD3rbhN6O4sWLUrv3r23eD4AAACg/miQAeX//J//k29/+9tJkkMPPTT33XffBrfevNUee+yRZO0tOSXLli2rbW/JLT/rdOzYcYvHAgAAAA1Lg7uFZ/To0fnqV7+aJHnf+96X+++/P+3bt9/sOevixrJly/LKK69sduy6K0nat2+/xc8/AQAAABq3BhVQ/vu//zunn3563nzzzRxwwAF54IEHtujKj/XfzDNr1qy3HVdXV5c5c+YkSbp37/7uFwwAAAA0Cg0moDzwwAM59dRTU1dXl/e85z35zW9+k4MPPniLzj3mmGNq2xMnTnzbcdOnT6/dwtO3b993t2AAAACg0WgQAeWRRx7JwIEDs2rVquy555751a9+lcMPP3yLzz/uuOOy1157JUl+9KMfpVqtbnLcqFGjatunnHLKu1ozAAAA0HjU+4Dyhz/8ISeddFKWLVuW1q1b5957781RRx21VXM0b948X/va15IkM2fOzA033LDRmClTpmTkyJFJkn79+qVXr17vfvEAAABAo7Bd38Lz8MMPZ/bs2bWvlyxZUtuePXv2Bld8JMmZZ565wddz5szJJz/5ydqDX6+44orstddeefLJJ9/2e+67777Zd999N9p/4YUX5vbbb88zzzyTiy66KLNnz87gwYPTqlWrTJgwIVdddVXq6urSqlWr3HzzzVv9WQEAAIDGq1J9u/tZtoEzzzwzP/rRj7Z4/FuXMmrUqJx11llb9T2/+93v5rLLLtvksdmzZ6d///559tlnN3l8zz33zE9+8pMMGDBgq77nlliwYEE6deqUZO2bfrz2eNfQ+VvjdvYSgO1k3jUn7ewlAACwCdvr9+96fwvPtvT+978/jz/+eK699tr07Nkzbdu2ze67755DDz003/jGNzJjxoztEk8AAACAhm27XoHC/3AFyq7JFSjQeLkCBQCgfnIFCgAAAMBOIqAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQ0GxnLwAAAOqTzt8at7OXAGwn8645aWcvgQbMFSgAAAAABQIKAAAAQIGAAgAAAFAgoAAAAAAUCCgAAAAABQIKAAAAQIGAAgAAAFAgoAAAAAAUCCgAAAAABQIKAAAAQIGAAgAAAFAgoAAAAAAUCCgAAAAABQIKAAAAQIGAAgAAAFAgoAAAAAAUCCgAAAAABQIKAAAAQIGAAgAAAFAgoAAAAAAUCCgAAAAABQIKAAAAQMF2DSiLFy/OPffck0svvTQnnnhi9tlnn1QqlVQqlZx55plbPd/48eMzaNCgdOzYMS1atEjHjh0zaNCgjB8/fovnWL58ea6//vr07t077dq1S5s2bdK9e/dccMEF+fOf/7zVawIAAAAav2bbc/L99ttvm8xTrVbz5S9/OcOHD99g/8KFCzNmzJiMGTMm5557bm699dZUKpW3nWfOnDk56aST8vTTT2+wf9asWZk1a1ZGjBiRn/70p+nfv/82WTcAAADQOOywW3g6deqUE0444R2de8kll9TiSY8ePTJ69OhMmzYto0ePTo8ePZIkw4cPz3e+8523neP111/PgAEDavHknHPOyQMPPJBHHnkkV155Zdq0aZNXX301n/nMZzJjxox3tE4AAACgcdquV6Bceuml6dWrV3r16pX99tsv8+bNS5cuXbZqjtmzZ+e6665LkvTs2TOTJk1Kq1atkiS9evXKySefnH79+mX69Om59tprc9ZZZ+Xggw/eaJ4bbrghs2bNSpJcd911ufDCC2vHjj766Bx//PH5yEc+kuXLl2fo0KF58MEH3+nHBgAAABqZ7XoFyuWXX54BAwa8q1t5brrpptTV1SVJhg0bVosn6+y+++4ZNmxYkqSuri4333zzRnO88cYb+f73v58k6d69e775zW9uNOboo4/O2WefnSSZMGFCHnvssXe8ZgAAAKBxqddv4alWq7nrrruSJN26dUufPn02Oa5Pnz459NBDkyRjx45NtVrd4PhDDz2UV155JUlyxhlnpEmTTX/s9R9s+8tf/vJdrh4AAABoLOp1QJk7d24WLlyYJOnXr99mx647vmDBgsybN2+DY5MnT95o3Kb07NkzrVu3TpI8/PDD72TJAAAAQCNUrwPKzJkza9vdunXb7Nj1j69/3tbM06xZs9rzU946BwAAALDr2q4PkX235s+fX9vu2LHjZsd26tRpk+et/3Xr1q3Ttm3b4jwzZszISy+9lFWrVqVFixZbtNYFCxZs9viiRYu2aB4AAACg/qnXAWXp0qW17TZt2mx27Lpbb5K1ryze1DylOTY1z5YGlPUDDgAAANC41OtbeFauXFnbbt68+WbHrh86VqxYscl5SnOU5gEAAAB2TfX6CpSWLVvWtlevXr3ZsatWraptv/VVx+vmKc1Rmmdz3nrb0FstWrQovXv33uL5AAAAgPqjXgeUPfbYo7b91tty3mrZsmW17bfeqrNuntIcpXk2p/SMFgAAAKDhqte38KwfJUoPaV3/CpC3Po9k3TzLli3LK6+8skXztG/ffouffwIAAAA0bvU6oBx22GG17VmzZm127PrHu3fv/o7mqaury5w5czY5BwAAALDrqtcBpUuXLunQoUOSZOLEiZsdO2nSpCTJgQcemM6dO29w7Jhjjqltb26e6dOn127h6du37ztZMgAAANAI1euAUqlUMnDgwCRrrxyZOnXqJsdNnTq1dmXJwIEDU6lUNjh+3HHHZa+99kqS/OhHP0q1Wt3kPKNGjaptn3LKKe92+QAAAEAjUa8DSpIMHTo0zZqtfdbtkCFDNnq18IoVKzJkyJAkSbNmzTJ06NCN5mjevHm+9rWvJUlmzpyZG264YaMxU6ZMyciRI5Mk/fr1S69evbblxwAAAAAasO36Fp6HH344s2fPrn29ZMmS2vbs2bM3uOIjSc4888yN5ujatWsuuOCCXHPNNZk+fXr69u2biy++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f8no0aPz0EMPbXRs5cqVte3mzZtv9vu0aNGitr1ixYp3vmAAAACg0WgQV6AsW7Ys/fv3z6RJk9K0adNcdNFFOeuss3LQQQdl5cqV+d3vfpf//b//dx5++OH84z/+Y2666aZ8/etfr53fsmXL2vb6b/TZlPXf3vPWVx1vTul2n0WLFqV3795bPB8AAABQfzSIgPLd7343kyZNSpKMHDlyg9t3mjdvnk984hM5/vjjc8IJJ2TChAn513/91xx//PE54ogjkiR77LFHbXzptpxly5bVtku3+6yv9GwVAAAAoOGq97fwVKvV/PCHP0yy9nXGb332yTrNmjXLv/3bvyVJ3nzzzdo5yYZxo/Sw1/WvJPFcEwAAACBpAAHlL3/5S/72t78lSXr06LHZsUcddVRte9asWbXtww47bJP7N2X94927d9+qtQIAAACNU70PKM2a/c9dRnV1dZsd+8Ybb2zyvC5duqRDhw5JkokTJ252jnW3Ch144IHp3Lnz1i4XAAAAaITqfUBp165d9txzzyTJlClTNhtR1o8jXbp0qW1XKpUMHDgwydorTKZOnbrJ86dOnVq7AmXgwIGpVCrvev0AAABAw1fvA0qTJk1y0kknJUleeOGFXHnllZsc9/LLL+fiiy+ufT1gwIANjg8dOrR2VcqQIUM2ekXxihUrMmTIkCRrr14ZOnTotvoIAAAAQANX7wNKklx66aXZfffdkySXXXZZTj755Nx55515/PHHM2XKlNx000350Ic+lD/96U9Jko997GM54YQTNpija9euueCCC5Ik06dPT9++fXP77bdn+vTpuf3229O3b99Mnz49SXLhhRfmkEMO2YGfEAAAAKjPGsRrjLt165a77rorp512WpYsWZK77747d9999ybHfvSjH80vfvGLTR678sors3jx4tx22215/PHHM3jw4I3GnH322bniiiu26foBAACAhq1BXIGSJB//+Mcza9asXHvttTnuuOPSvn377LbbbmnVqlW6dOmSU089NWPHjs3999+fvffee5NzNGnSJCNHjsy4ceMycODAdOjQIc2bN0+HDh0ycODA3HvvvRkxYkSaNGkwfy0AAADADtAgrkBZ5z3veU8uuuiiXHTRRe9qnv79+6d///7baFUAAABAY+dSCwAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoaXEBZsmRJrrvuuvTt2zf7779/WrRokQ4dOuTDH/5wLrzwwkyZMqU4x/jx4zNo0KB07NgxLVq0SMeOHTNo0KCMHz9+B3wCAAAAoKFptrMXsDV+8Ytf5Ctf+Ur++te/brB/0aJFWbRoUaZNm5Znn302Y8eO3eT51Wo1X/7ylzN8+PAN9i9cuDBjxozJmDFjcu655+bWW29NpVLZXh8DAAAAaGAaTED58Y9/nLPOOitvvvlm9t1333zlK1/JMccck3bt2uXFF1/MnDlzcvfdd2e33XZ72zkuueSSWjzp0aNHLrroohx88MGZM2dOrrvuujz++OMZPnx42rdvnyuuuGJHfTQAAACgnmsQAWXmzJk599xz8+abb+bYY4/N3Xffnb322mujcUOGDMnq1as3Ocfs2bNz3XXXJUl69uyZSZMmpVWrVkmSXr165eSTT06/fv0yffr0XHvttTnrrLNy8MEHb78PBQAAADQYDeIZKEOGDMmqVauyzz775Je//OUm48k6zZs33+T+m266KXV1dUmSYcOG1eLJOrvvvnuGDRuWJKmrq8vNN9+8bRYPAAAANHj1PqDMmjUrDzzwQJLk/PPPzz777LPVc1Sr1dx1111Jkm7duqVPnz6bHNenT58ceuihSZKxY8emWq2+w1UDAAAAjUm9Dyi/+MUvatuf+cxnatsvv/xynn322Y0eKLspc+fOzcKFC5Mk/fr12+zYdccXLFiQefPmvYMVAwAAAI1NvQ8oU6dOTZLstdde6d69e37yk5/k7/7u79KuXbt07do1++yzTw466KBcfvnlef311zc5x8yZM2vb3bp12+z3W//4+ucBAAAAu656/xDZP/3pT0mSzp07Z8iQIfnP//zPjcbMnTs3l112We6444786le/SocOHTY4Pn/+/Np2x44dN/v9OnXqtMnzShYsWLDZ44sWLdriuQAAAID6pd4HlL/97W9J1j4L5Yknnkjbtm1zzTXXZNCgQdlzzz3zxz/+MZdeemnuu+++PPnkk/nMZz6TyZMnp0mT/7m4ZunSpbXtNm3abPb7tW7durb9dle0bMr64QUAAABoXOr9LTzLli1LkqxatSpNmzbNfffdl/POOy/t27dPixYt0rNnz9xzzz058cQTkySPPPJIfvnLX24wx8qVK2vbb/eWnnVatGhR216xYsW2+hgAAABAA1bvr0Bp2bJlLaJ85jOf2eQbdJo0aZLrr78+9913X5Jk9OjR+fSnP73BHOusXr16s99v1apVte23vup4c0q3+yxatCi9e/fe4vkAAACA+qPeB5Q99tijFlDWXWWyKYcffngOPPDALFy4MI8++uhGc6xTui1n3fdKyrf7rK/0bBUAAACg4ar3t/Cs/2yRLX0A7OLFizfYv/55pYe9rn8lieeaAAAAAEkDCCiHH354bXvNmjWbHbvueLNmG15Yc9hhh9W2Z82atdk51j/evXv3LV4nAAAA0HjV+4DykY98pLY9Z86czY597rnnkiQHHnjgBvu7dOlSe7XxxIkTNzvHpEmTanN07tx5a5cLAAAANEL1PqCcfPLJ2W233ZJko7frrG/ixIn561//miQ59thjNzhWqVQycODAJGuvMJk6deom55g6dWrtCpSBAwemUqm86/UDAAAADV+9Dyjvec978qUvfSlJ8pvf/CY/+9nPNhqzdOnSDB06tPb1eeedt9GYoUOH1m7tGTJkyEavKF6xYkWGDBmSZO0tQOvPBwAAAOza6n1ASZLLL788733ve5MkX/jCFzJkyJBMmDAhjz32WEaNGpXevXvnD3/4Q5LkK1/5Snr16rXRHF27ds0FF1yQJJk+fXr69u2b22+/PdOnT8/tt9+evn37Zvr06UmSCy+8MIcccsiO+XAAAABAvVfvX2OcJO3bt8/48eNz8sknZ/bs2fmP//iP/Md//MdG4774xS/m+9///tvOc+WVV2bx4sW57bbb8vjjj2fw4MEbjTn77LNzxRVXbNP1AwAAAA1bg7gCJVn7Rpw//OEPuf766/PhD3847dq1S/PmzdOxY8d89rOfzYMPPpiRI0fWnpeyKU2aNMnIkSMzbty4DBw4MB06dEjz5s3ToUOHDBw4MPfee29GjBiRJk0azF8LAAAAsAM0iCtQ1mndunUuuOCC2q0471T//v3Tv3//bbQqAAAAoLFzqQUAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFDTqgXHTRRalUKrU/Dz30UPGc8ePHZ9CgQenYsWNatGiRjh07ZtCgQRk/fvz2XzAAAADQIDXYgPLEE0/kpptu2uLx1Wo15513Xk488cSMGTMmCxcuzOrVq7Nw4cKMGTMmJ554Ys4777xUq9XtuGoAAACgIWqQAeXNN9/MOeeck7q6uuy7775bdM4ll1yS4cOHJ0l69OiR0aNHZ9q0aRk9enR69OiRJBk+fHi+853vbLd1AwAAAA1Tgwwo//7v/55HH3003bp1y9lnn10cP3v27Fx33XVJkp49e+a3v/1tBg8enF69emXw4MF5+OGH07NnzyTJtddemzlz5mzX9QMAAAANS4MLKPPnz69dJXLLLbekefPmxXNuuumm1NXVJUmGDRuWVq1abXB89913z7Bhw5IkdXV1ufnmm7ftogEAAIAGrcEFlK9+9at5/fXXc8YZZ+S4444rjq9Wq7nrrruSJN26dUufPn02Oa5Pnz459NBDkyRjx471LBQAAACgpkEFlJ///Oe555570q5du1x//fVbdM7cuXOzcOHCJEm/fv02O3bd8QULFmTevHnvaq0AAABA49FgAsorr7ySr3/960nWPqekffv2W3TezJkza9vdunXb7Nj1j69/HgAAALBra7azF7ClLrroorz44ov5+7//+y16cOw68+fPr2137Nhxs2M7deq0yfO2xIIFCzZ7fNGiRVs1HwAAAFB/NIiA8vDDD2fEiBFp1qxZbr311lQqlS0+d+nSpbXtNm3abHZs69ata9uvv/76Vq1x/fgCAAAANC71/hae1atX59xzz021Ws03vvGNfPCDH9yq81euXFnbLr2xp0WLFrXtFStWbN1CAQAAgEar3l+BctVVV2XmzJl573vfm+9+97tbfX7Lli1r26tXr97s2FWrVtW23/qq45LSLT+LFi1K7969t2pOAAAAoH6o1wFl1qxZufrqq5Mkw4YN2+AWmy21xx571LZLt+UsW7astl263eetSs9XAQAAABqueh1QbrrppqxevToHHXRQli9fnp/97GcbjXnyySdr2w8++GBefPHFJMk//uM/pnXr1huEjdKDXte/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+21ybMuWLWvb6z9wdlNWrVpV237rq443p3S7z6JFi9K7d+8tng8AAACoPxpkQJk7d25OOOGEvPzyy2natGlGjx692bfr7LHHHrXt0m05y5Ytq22XbvdZX+nZKgAAAEDD1eBu4XnhhRfy8Y9/PC+88EIqlUpuu+22nHLKKZs9Z/24UXrY6/pXkniuCQAAAJA0sICyZMmSfOITn8hzzz2XJBk2bFhOP/304nmHHXZYbXvWrFmbHbv+8e7du7/DlQIAAACNSYMJKK+++mo++clP5k9/+lOS5Jprrsm//Mu/bNG5Xbp0SYcOHZKsffDs5kyaNClJcuCBB6Zz587vfMEAAABAo9EgAsry5ctz0kkn5fe//32S5P/7//6/XHzxxVt8fqVSycCBA5OsvcJk6tSpmxw3derU2hUoAwcOTKVSeZcrBwAAABqDeh9QVq9enVNOOSW//e1vkyRf//rXc8UVV2z1PEOHDk2zZmufmTtkyJCNXlG8YsWKDBkyJEnSrFmzDB069N0tHAAAAGg06v1beE477bT8+te/TpJ89KMfzdlnn50nn3zybcc3b948Xbt23Wh/165dc8EFF+Saa67J9OnT07dv31x88cU5+OCDM2fOnFx77bV5/PHHkyQXXnhhDjnkkO3zgQAAAIAGp94HlF/+8pe17QcffDBHHHHEZse/733vy7x58zZ57Morr8zixYtz22235fHHH8/gwYM3GnP22We/oytcAAAAgMar3t/Csy01adIkI0eOzLhx4zJw4MB06NAhzZs3T4cOHTJw4MDce++9GTFiRJo02aX+WgAAAICCen8FSrVa3eZz9u/fP/3799/m8wIAAACNk0stAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKNglA8qf//znXHDBBenevXtat26ddu3apXfv3rnhhhuyfPnynb08AAAAoJ5ptrMXsKONGzcun/vc5/Lqq6/W9i1fvjyPPvpoHn300YwYMSL33ntvDjrooJ24SgAAAKA+2aWuQHniiSdy6qmn5tVXX02bNm1y5ZVX5pFHHskDDzyQc845J0ny9NNP56STTsrrr7++k1cLAAAA1Be71BUoQ4cOzfLly9OsWbP8+te/ztFHH1079tGPfjSHHHJILrroosyaNSvf+973cumll+7E1QIAAAD1xS5zBcqjjz6ahx56KEly9tlnbxBP1vnmN7+Z7t27J0luvvnmvPHGGztyiQAAAEA9tcsElLFjx9a2zzrrrE2OadKkSU4//fQkycsvv1wLLgAAAMCubZcJKJMnT06StG7dOkcdddTbjuvXr19t++GHH97u6wIAAADqv10moMycOTNJ8v73vz/Nmr39o1+6deu20TkAAADArm2XeIjsypUrs2TJkiRJx44dNzt27733TuvWrbNs2bLMnz9/i7/HggULNnt8/bkWLVq0xfPSsNW9tmRnLwHYTkr/3QcaLj+/ofHy83vXsP7v3HV1ddts3l0ioCxdurS23aZNm+L4dQFla15l3KlTpy0e27t37y0eC0D91OmWnb0CAGBr+fm963nppZfSuXPnbTLXLnELz8qVK2vbzZs3L45v0aJFkmTFihXbbU0AAABAw7FLXIHSsmXL2vbq1auL41etWpUkadWq1RZ/j9LtPitXrsysWbOy3377pX379pt9DgvQsCxatKh2Zdm0adNywAEH7OQVAQAlfn5D41VXV5eXXnopSfLBD35wm827S/wWv8cee9S2t+S2nGXLliXZstt91ik9WyVZ+wBboHE74IADtui/BwBA/eHnNzQ+2+q2nfXtErfwtGzZMvvss0+S8kODXn755VpA2ZrnmgAAAACN1y4RUJKke/fuSZLZs2dv9im8s2bN2ugcAAAAYNe2ywSUY445Jsna23Mee+yxtx03ceLE2nbfvn23+7oAAACA+m+XCSif+tSnats//OEPNznmzTffzI9//OMkSdu2bXP88cfviKUBAAAA9dwuE1B69+6dY489NkkycuTITJkyZaMxN954Y2bOnJkk+frXv57ddttth64RAAAAqJ92ibfwrPP9738/ffv2zYoVK3LCCSfk29/+do4//visWLEiP/vZzzJ8+PAkSdeuXfPNb35zJ68WAAAAqC92qYDSo0eP3H777fn85z+f1157Ld/+9rc3GtO1a9eMGzdug1cfAwAAALu2SrVare7sRexozz//fL7//e9n3LhxWbBgQZo3b573v//9+cxnPpPzzz8/u++++85eIgAAAFCP7JIBBQAAAGBr7DIPkQUAAAB4pwQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoaLazFwDQWM2ZMydLlixJ586ds99+++3s5QBAo/bFL35xm89ZqVQycuTIbT4v0DBVqtVqdWcvAqAheemll/KLX/wiSfK5z30ue+211wbHZ8+enc9+9rP5wx/+kGTt/3x96lOfyogRI9K2bdsdvFoA2DU0adIklUplm81XrVZTqVSyZs2abTYn0LAJKABb6dZbb81Xv/rVHHrooZk5c+YGx1atWpUPfOADee6557L+f14rlUqOPfbYPPTQQzt4tQCwa+jcufM2DSjrzJ07d5vPCTRMbuEB2Eq//vWvU6lU8k//9E8bHRs1alTmzJmTSqWSk08+OR/72Mdy//335+67787kyZPz85//PKeeeupOWDUANG7z5s3b2UsAGjkPkQXYSk8//XSSpHfv3hsdGz16dJLkox/9aMaOHZshQ4bkrrvuysc//vFUq9XacQAAoGERUAC20ksvvZQk6dChwwb7V6xYkSlTpqRSqeTcc8/d4Ni6B9v9/ve/3zGLBAAAtikBBWArvfLKK0nWPqxufVOnTs0bb7yRSqWSj3/84xsc69KlS5Jk8eLFO2SNAADAtiWgAGylNm3aJElefPHFDfave0DsYYcdlr333nuDY7vttluSpFkzj54CAICGyP/JA2ylbt265Xe/+13Gjx+f/v371/bfeeedqVQq6dev30bnrIst++233w5bJwDsSg466KAka998N2fOnI32vxNvnQvYtQkoAFvppJNOytSpUzN8+PB07949xx57bEaNGpU//elPqVQqGTRo0EbnrHv2SceOHXf0cgFgl7DuLTxvfZXxu3k7z/Z4LTLQcAkoAFvp/PPPzw9+8IMsWrQo559//gbHjj766Bx//PEbnXP33XenUqnk2GOP3VHLBIBdyhlnnLFV+wG2VqVarVZ39iIAGpqZM2fmC1/4wgZv1Tn22GMzevTojd7O88QTT6RHjx6pVCqZMGFCPvKRj+zo5QIAAO+SgALwLsydOzcvvvhiDjjggHTu3HmTY5544on84Q9/SJJ87nOf8yBZAABogAQUAAAAgAKvMQYAAAAocB05wHZw99135+c//3mWLFmSLl265JxzzkmPHj129rIAgKx9M8+SJUuyYsWKlC7I9+wyYB238ABspQkTJuSzn/1sWrZsmRkzZqRt27YbHP/Od76Tq666aoN9TZs2zQ9/+MN87nOf24ErBQDWefrpp3PVVVflv//7v/Paa69t0TmVSiV1dXXbeWVAQ+EWHoCtdO+992bJkiXp06fPRvFkxowZueqqq1KtVlOtVtO2bdtUq9XU1dXl3HPPzfPPP79zFg0Au7CxY8fmyCOPzH/913/l1Vdfrf2c3pI/AOsIKABb6eGHH06lUsknPvGJjY7dcsstqVar2XvvvfPYY4/lr3/9a6ZNm5Z27dpl5cqVufXWW3fCigFg1zV//vx8/vOfz4oVK9KhQ4fcfPPNGT58eJK1V5g88MADueOOO/Ktb30rHTp0SJIcc8wxuf/++/Pggw/uzKUD9YyAArCVXnzxxSRJt27dNjp2zz33pFKp5F/+5V9qzzzp2bNnzj///FSr1dx///07dK0AsKv793//9yxfvjx77LFHfve73+VrX/tajj766Nrx448/PoMGDcpVV12VZ599NoMHD85vf/vbjBw5Mv369duJKwfqGwEFYCstXrw4SbLXXnttsH/OnDlZuHBhkmTQoEEbHDv22GOTJLNnz94BKwQA1rn//vtTqVTy1a9+tXaFydtp1apV/uu//is9evTIz372s9x55507aJVAQyCgAGyldfdDv/rqqxvsnzx5cpK1YeVDH/rQBsfe8573JEmWL1++/RcIANTMmzcvSfL3f//3tX2VSqW2/daHxDZp0iRf+9rXUq1Wc9ttt+2QNQINg4ACsJX233//JMnMmTM32P+rX/0qSdK3b9+Nzlm2bFmSZO+9997OqwMA1rfuZ3CnTp1q+3bffffa9lv/QSRJDj/88CTJE088sZ1XBzQkAgrAVurTp0+q1WpuueWW2hUlzz33XO666663fbjsM888k+R/4gsAsGOsu+V25cqVtX3rrgxN1t6C+1brXnO8ZMmS7bw6oCERUAC20pe+9KUka19Z/IEPfCCf/vSn06dPn6xcuTKtWrXKP//zP290zqRJk5Ikhx122A5dKwDs6g499NAka/+xY5099tgj73vf+5Ikv/71rzc6Z91D39u2bbv9Fwg0GAIKwFb66Ec/mqFDh6ZarWbevHkZM2ZM7V+orr/++uyzzz4bjF+5cuVmr04BALafdW/cmTp16gb7BwwYkGq1muuvv36D1xXfcccdufnmm1OpVDZ5Wy6w66pU1z0NEYCtcs899+QXv/hFXnzxxRxwwAE5/fTT89GPfnSjcT//+c9z0UUXpVKpZPLkyenYseNOWC0A7JomTJiQj33sY+nQoUOef/75NG3aNEny5z//OYcddlhWrFiRJGnXrl1WrVqVZcuWpVqtpmnTppk8eXL69OmzM5cP1CMCCgAA0GhVq9VcfvnlWbNmTc4555y8973vrR2777778rnPfS6vvPLKBue0aNEit9xyS84888wdu1igXhNQAACABu+///u/kyQf+9jH0rp16y0+729/+1t+8Ytf5KmnnkpdXV0OOeSQnHrqqTnwwAO311KBBkpAAQAAGrwmTZqkSZMmmTFjxgYPbf/iF7+YSqWSK664IgcccMBOXCHQ0AkoANvAmjVr8vLLL2fFihUp/Wd1/UuHAYBto0mTJqlUKvnjH/+4QUB5u/0AW6vZzl4AQEO1ZMmSDBs2LGPHjs2f/vSnvPnmm8VzKpVK6urqdsDqAGDX0qJFi6xevTqvv/76zl4K0EgJKADvwCOPPJJBgwblpZdeKl5xAgBsfwceeGDmzp2byZMnp3fv3jt7OUAjJKAAbKW//vWvGThwYP7617+mTZs2+dKXvpS2bdvmsssuS6VSyYgRI/Lyyy9n+vTpueuuu7Jy5cr07ds3Z5999s5eOgA0Wh/72Mfyf//v/823v/3tTJs2LV27ds1uu+1WO/6DH/wg++6771bPe+mll27LZQINmGegAGylyy+/PJdffnlatGiR6dOn5/DDD89TTz2VD37wg6lUKlmzZk1t7Isvvph//ud/zsSJE3PBBRfk2muv3YkrB4DGa/78+TnyyCPz17/+NZVKpbZ/3a876+/bGuv/XAd2bU129gIAGpr77rsvlUolX/ziF3P44Ydvduz++++fcePG5eCDD84NN9yQBx98cAetEgB2LZ06dcrvf//7fOlLX0rnzp2z2267pVqt1sJJtVp9R38A1hFQALbS7NmzkyQf//jHa/vW/1ett/5LVatWrfKNb3wj1Wo1t956645ZJADsgjp16pThw4dnzpw5WblyZd58881aRHnyySfz5ptvbvUfgHUEFICt9NprryVJ3ve+99X2tWzZsra9dOnSjc7p2bNnkuR3v/vddl4dAACwPXiILMBWatOmTV599dUNXkfcrl272va8efPyoQ99aINzVq5cmSRZvHjxDlkjALDWD3/4wyRJx44dd/JKgIbOFSgAW+n9739/kuTPf/5zbV/btm2z//77J0kmTJiw0TmPPPJIkqR169Y7YIUAwDpnnHFGzjjjjOy55547eylAAyegAGylD3/4w0mSRx99dIP9//AP/5BqtZrrrrsuzzzzTG3/tGnTct1116VSqaRXr147dK0AAMC24TXGAFvpnnvuycknn5yDDz44zz77bG3/k08+mSOPPDJr1qxJ06ZN83d/93dZvnx5nnnmmaxZsyaVSiXjxo3LP/zDP+zE1QMAAO+EK1AAttInP/nJnH766enTp0/mzp1b2/+BD3wgt9xyS5o2bZq6uro89thjmTlzZu2tPJdddpl4AgAADZQrUAC2saeffjqjRo3KU089lbq6uhxyyCH5whe+UHsTDwAA0PAIKAAAAAAFXmMMsI3U1dXl5ZdfTpLsvffeadbMf2IBAKCx8AwUgHfhqaeeypAhQ9K9e/e0bNky+++/f/bff/+0bNky3bt3z5AhQ/Lkk0/u7GUCAADvklt4AN6BN998M//6r/+a//zP/8ybb76Zt/tPaaVSSZMmTXL++efnxhtvTJMmujUAADREAgrAO3DqqafmzjvvrIWTww8/PL17985+++2XarWaxYsX59FHH61dfVKpVPLpT386t99++85cNgAA8A4JKABb6ac//Wk+//nPp1Kp5Igjjsjw4cPTq1evTY6dPn16zjvvvDz++OOpVCr5yU9+ksGDB+/gFQMAAO+WgAKwlY4//vhMnDgxhx56aKZPn57WrVtvdvyyZcvSs2fPPP300+nXr18mTJiwg1YKAABsK27GB9hKM2bMSKVSycUXX1yMJ0nSunXrXHzxxUmSJ554YnsvDwAA2A4EFICttHr16iTJEUccscXnrBv7xhtvbJc1AQAA25eAArCV3ve+9yVJXn311S0+57XXXtvgXAAAoGERUAC20j/90z+lWq3mzjvv3OJz7rjjjlQqlZxyyinbcWUAAMD24iGyAFvp1VdfzVFHHZXnn38+P/nJT3Lqqadudvwdd9yR0047Le973/vy2GOPZa+99tpBKwUAALYVV6AAbKW99tor999/f4488sicdtpp+dSnPpWxY8dm4cKFeeONN1JXV5eFCxdm7NixOeWUU/LZz342Rx55ZB544AHxBAAAGihXoABspaZNm9a2q9VqKpXKZsdvyZhKpZK6urptsj4AAGDba7azFwDQ0Ly1O29Jh9aqAQCgYRNQALbSd7/73Z29BAAAYAdzCw8AAABAgYfIAgAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACADR4o0aNSqVSSaVSybx583b2ct5W586dU6lUcuaZZ+7spQAAW0lAAQAAACgQUAAAAAAKBBQAAACAAgEFAGiwHnrooVQqlZx11lm1fV26dKk9D2Xdn4ceemijc3/zm9/k85//fLp06ZJWrVplzz33zN/93d/loosuyqJFizb7fV944YV861vfypFHHpm99torzZs3z/77758PfvCDOe200zJq1Ki89tprtfHHHXdcKpVKnn/++STJj370o43WeNxxx22TvxMAYPtotrMXAACwIy1btixf+MIXMmbMmA32r1y5MjNmzMiMGTNyyy23ZPTo0RkwYMBG50+ePDkDBgzYIJAkyV/+8pf85S9/yZNPPpmf/exn2WeffTZ5PgDQMFWq1Wp1Zy8CAOCdWLZsWebOnZu77rorl1xySZLkV7/6VTp06LDBuC5duqR169ZZs2ZNPvGJT2TChAmpVCoZPHhwBg0alC5duuSNN97ItGnTcuONN+bPf/5zmjdvnkceeSRHHXVUbZ5Vq1bloIMOygsvvJA99tgjX/nKV3L88cdn3333zRtvvJHnn38+U6ZMyZ133pkf/OAHtYAyd+7cLFu2LJ/85CfzwgsvZODAgbniiis2WGPr1q3TpUuX7fw3BgC8UwIKANDgjRo1qnYbz9y5c9O5c+dNjrvxxhtzwQUXZLfddstdd92VE088caMxL7/8co499tg89dRTOeaYYzJ58uTasQcffDAf+9jHkiR33333215hUldXl+XLl2fPPffcYH/nzp3z/PPP54wzzsioUaPewScFAHYWz0ABAHYJb7zxRm688cYkyfnnn7/JeJIke++9d66//vokycMPP5zZs2fXjr344ou17Y985CNv+72aNWu2UTwBABo2AQUA2CVMmzat9nDYU089dbNj148jU6ZMqW0fcMABte0f/vCH23iFAEB9JqAAALuE6dOn17aPPvrojd6Cs/6fNm3a1Mauf9XJMccck4MOOihJMnTo0PTu3TtXX311HnnkkaxevXrHfRgAYIcTUACAXcLixYvf0XnLly+vbe+22265++6707179yTJo48+mm9/+9vp27dv2rZtmxNPPDE//elPs2bNmm2yZgCg/vAaYwBgl7B+1HjooYfynve8Z4vO23fffTf4+rDDDssf//jH3H333bn77rszceLEzJkzJytWrMj48eMzfvz4fO9738u999670bkAQMMloAAAu4T1g0nz5s3zgQ984B3P1bRp03zqU5/Kpz71qSTJokWLct999+UHP/hBHnvssTz22GM577zzMmbMmHe7bACgnnALDwDQ4FUqleKYHj161LZ//etfb9Pvf8ABB+SLX/xipkyZkiOPPDJJcs8992TFihVbvU4AoH4SUACABq9ly5a17VWrVm1yzDHHHJN27dolSW699da89tpr23wdu+22W/r165ckqauryyuvvLLJdb7dGgGA+ktAAQAavPVfLzxnzpxNjmnZsmUuuOCCJGvfrDN48OAsW7bsbedcunRp/uM//mODfZMnT87s2bPf9pzVq1dn4sSJSZI2bdqkffv2m1zn260RAKi/KtVqtbqzFwEA8G4sXbo0++67b1auXJkjjzwyV199dTp37pwmTdb+W9GBBx6YVq1aZc2aNfnkJz+ZBx54IEny3ve+N1/+8pdz9NFHp23btlm6dGmefvrpPPTQQxk7dmxatmyZJUuW1L7PZZddln/7t3/Lsccem5NOOilHHHFE2rdvnxUrVuSZZ57JrbfemmnTpiVZ+5rjm266aYN1XnLJJbnyyiuTJFdffXVOPPHEtG7dOknSqlWrHHjggdv97woAeGcEFACgUbj44otz3XXXbfLYhAkTctxxxyVJVqxYkS9/+cv58Y9/XJyzS5cuee6552pfX3bZZbn88suL5w0aNCg/+clPNri1KEkWLlyYI444In/72982Oqdfv3556KGHinMDADuHgAIANArVajUjR47Mj3/84zz11FN59dVXa68uXj+grPPYY49l5MiRmTRpUhYsWJBly5alTZs26dy5c4466qiceOKJGTBgQFq0aFE7Z/ny5Zk4cWJ+85vfZMqUKXnhhReyePHiJMn++++fD3/4wzn99NPTv3//t13nnDlzcvXVV2fixIlZsGBBVq5cmURAAYD6TkABAAAAKPAQWQAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAICC/x+HU+wi0w+E5wAAAABJRU5ErkJggg=="/>


```python
### 축 이름 회전하기

count_test.plot.bar(rot = 0)
```

<pre>
<Axes: xlabel='test'>
</pre>
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABFAAAANhCAYAAADABk+6AAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjcuMiwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8pXeV/AAAACXBIWXMAAB7CAAAewgFu0HU+AABNOklEQVR4nO3de5jWdYH//9fgcMYTiQZCgSSCVrsqEISKrmUrsk6wZdpuipmnNjba0Np+prhp5hFbKl0uMGy3yA6KqyjlETRhEVNJgxQCFaQIU0OOjszvDy7uL8Qwb1SQmeHxuC6v6zP35/153+97/vCGJ59DVV1dXV0AAAAA2KYWu3oBAAAAAI2dgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAXVu3oBu4u1a9fmN7/5TZKkU6dOqa72qwcAAIAdrba2Nn/605+SJB/4wAfSpk2bHTKvv8W/Q37zm9+kf//+u3oZAAAAsNuYPXt2+vXrt0PmcgkPAAAAQIEzUN4hnTp1qmzPnj07nTt33oWrAQAAgOZp2bJllStANv+7+NsloLxDNr/nSefOndO1a9dduBoAAABo/nbk/UddwgMAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAEBB9a5eADRn3b86dVcvAdhJFn/rpF29BAAA3kHOQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACnZqQFm+fHnuvPPOXHzxxTnxxBOz3377paqqKlVVVRkxYsR2zbF27drcfvvtGTlyZD70oQ+lY8eOadmyZTp27JiBAwdmzJgxWbZs2XavafXq1bn66qvTv3//dOzYMR06dEifPn0yevToPP/882/xkwIAAADNWfXOnPyAAw54W8fPnTs3Rx11VFauXLnVvpdffjmzZs3KrFmzct1112XChAk55ZRTGpxv4cKFOemkk/K73/1ui9fnz5+f+fPnZ8KECfnRj36UIUOGvK11AwAAAM3LO3YJT7du3XLCCSe8qWP+8pe/VOLJoEGDcsUVV+See+7Jr3/96/ziF7/Iueeemz322CMrV67Mpz/96dx9993bnOu1117L0KFDK/Hk7LPPzn333ZdHHnkkl19+eTp06JBXX301n/zkJzN37ty3/kEBAACAZmennoFy8cUXp1+/funXr18OOOCALF68OD169Nju41u0aJFTTjkll1xySQ499NCt9p9wwgk58cQTM2zYsLzxxhsZOXJknn322VRVVW019pprrsn8+fOTJFdddVUuuOCCyr6BAwfmuOOOyzHHHJPVq1dn1KhRuf/++9/CJwYAAACao516Bsqll16aoUOHvuVLeT784Q/nlltuqTeebFJTU5Phw4cn2XiJzhNPPLHVmNdffz3f/va3kyR9+vTJl7/85a3GDBw4MGeddVaS5IEHHshjjz32ltYMAAAAND/N4ik8xx13XGV74cKFW+1/8MEH88orryRJzjjjjLRoUf/H3vzGtrfeeusOXSMAAADQdDWLgLJu3brKdn1x5KGHHqpsDx48eJvz9O3bN+3bt0+SPPzwwztwhQAAAEBTtlPvgfJOmT59emW7d+/eW+2fN29eg/s3qa6uTs+ePTN37twtjtkeS5YsaXD/m3nUMgAAANC4NPmA8uSTT2bq1KlJksMOO6ze+6W88MILSZL27dtnn332aXC+bt26Ze7cufnTn/6UdevWpXXr1tu1jm7dur25hQMAAABNRpO+hGfdunX53Oc+lzfeeCNJ8s1vfrPecZsehdyhQ4finJsu4Uk2PvoYAAAAoEmfgfKFL3whc+bMSbLx5rAnn3xyvePWrl2bJGnVqlVxzs3POFmzZs12r2XTWS7bsmzZsvTv33+75wMAAAAajyYbUK644opMmDAhSXLkkUfmu9/97jbHtmnTJkmyfv364ryb35C2bdu2272erl27bvdYAAAAoGlpkpfw/Nd//Ve+9rWvJUkOOeSQ3H333VtcevPX9txzzyTbd0nOqlWrKtvbc8kPAAAA0Pw1uYAyefLkfP7zn0+SvPe97829996bTp06NXjMprNDVq1alVdeeaXBsZsuxenUqdN230AWAAAAaN6aVED53//935x++unZsGFDOnfunPvuu2+7Lp3Z/Mk88+fP3+a42traLFy4MEnSp0+ft79gAAAAoFloMgHlvvvuyymnnJLa2tq8613vyj333JOePXtu17FHHXVUZXv69OnbHDdnzpzKJTyDBg16ewsGAAAAmo0mEVAeeeSR1NTUZN26ddlrr73yi1/8Iocddth2H3/sscdm7733TpLcfPPNqaurq3fcpEmTKtvDhg17W2sGAAAAmo9GH1CeeOKJnHTSSVm1alXat2+fu+66K0ceeeSbmqNVq1b513/91yTJvHnzcs0112w1ZubMmZk4cWKSZPDgwenXr9/bXzwAAADQLOzUxxg//PDDWbBgQeXnFStWVLYXLFiwxRkfSTJixIgtfl64cGE+9rGPVW78etlll2XvvffOU089tc333H///bP//vtv9foFF1yQW265Jc8880wuvPDCLFiwIKeeemratm2bBx54IN/85jdTW1ubtm3b5vrrr3/TnxUAAABovqrqtnU9yw4wYsSI3Hzzzds9/q+XMmnSpJx55plv6j0vueSSjBkzpt59CxYsyJAhQ/Lss8/Wu3+vvfbKD3/4wwwdOvRNvef2WLJkSbp165Zk45N+tufmtzR93b86dVcvAdhJFn/rpF29BAAA6rGz/v7d6C/h2ZHe97735fHHH8+VV16Zvn37Zp999km7du1yyCGH5Etf+lLmzp27U+IJAAAA0LTt1DNQ+H+cgbJ7cgYKNF/OQAEAaJycgQIAAACwiwgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAA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AAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgoEkHlAsvvDBVVVWV/x588MHiMdOmTcvw4cPTtWvXtG7dOl27ds3w4cMzbdq0nb9gAAAAoElqsgHlySefzNixY7d7fF1dXc4999yceOKJue2227J06dKsX78+S5cuzW233ZYTTzwx5557burq6nbiqgEAAICmqEkGlA0bNuTss89ObW1t9t9//+065qKLLsr48eOTJIcffngmT56c2bNnZ/LkyTn88MOTJOPHj8/Xv/71nbZuAAAAoGlqkgHlP//zP/Poo4+md+/eOeuss4rjFyxYkKuuuipJ0rdv3/zqV7/Kqaeemn79+uXUU0/Nww8/nL59+yZJrrzyyixcuHCnrh8AAABoWppcQHnhhRcqZ4nccMMNadWqVfGYsWPHpra2Nkkybty4tG3bdov97dq1y7hx45IktbW1uf7663fsogEAAIAmrckFlM9//vN57bXXcsYZZ+TYY48tjq+rq8vtt9+eJOndu3cGDBhQ77gBAwbkkEMOSZJMmTLFvVAAAACAiiYVUH7yk5/kzjvvTMeOHXP11Vdv1zGLFi3K0qVLkySDBw9ucOym/UuWLMnixYvf1loBAACA5qN6Vy9ge73yyiv54he/mGTjfUo6deq0XcfNmzevst27d+8Gx26+f968eenRo8d2r2/JkiUN7l+2bNl2zwUAAAA0Lk0moFx44YX5wx/+kA9/+MPbdePYTV544YXKdteuXRsc261bt3qP2x6bHwsAAAA0L03iEp6HH344EyZMSHV1dW688cZUVVVt97ErV66sbHfo0KHBse3bt69sv/baa29+oQAAAECz1OjPQFm/fn3OOeec1NXV5Utf+lI+8IEPvKnj165dW9kuPbGndevWle01a9a8qfcpnbGybNmy9O/f/03NCQAAADQOjT6gfPOb38y8efPynve8J5dccsmbPr5NmzaV7fXr1zc4dt26dZXtv37UcUnp8iAAAACg6WrUl/DMnz8/V1xxRZJk3LhxW1xis7323HPPynbpspxVq1ZVtkuX+wAAAAC7j0Z9BsrYsWOzfv36HHTQQVm9enV+/OMfbzXmqaeeqmzff//9+cMf/pAk+Yd/+Ie0b99+izNDSk/K2fwyHDeF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3LnzLl4RAFDi+xuar9ra2vzpT39KknzgAx/YYfPuFn+Lb9OmTWV7/fr1xfHr1q1LkrRt23a736N0aVCy8f4rQPPWuXPn7fr/AQDQePj+huZnR122s7nd4hKePffcs7K9PZflrFq1Ksn2Xe4DAAAANH+7RUBp06ZN9ttvvyTluy6//PLLlYDyZm4MCwAAADRfu0VASZI+ffokSRYsWNDgY4zmz5+/1TEAAADA7m23CShHHXVUko2X5zz22GPbHDd9+vTK9qBBg3b6ugAAAIDGb7cJKB//+Mcr29///vfrHbNhw4b84Ac/SJLss88+Oe64496JpQEAAACN3G4TUPr375+jjz46STJx4sTMnDlzqzHXXntt5s2blyT54he/mJYtW76jawQAAAAap93iMcabfPvb386gQYOyZs2anHDCCfna176W4447LmvWrMmPf/zjjB8/PknSq1evfPnLX97FqwUAAAAai6q6urq6Xb2Id9Idd9yRf/7nf85f/vKXevf36tUrU6dOzfve9753eGUAAABAY7XbBZQkee655/Ltb387U6dOzZIlS9KqVau8733vyyc/+cl84QtfSLt27Xb1EgEAAIBGZLcMKAAAAABvxm5zE1kAAACAt0pAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAABosp5//vmce+656dmzZ9q0aZOqqqpUVVVlypQpO2T+ESNGpKqqKt27d693f/fu3VNVVZURI0bskPcDGq/qXb0AAACAt+L555/PkUcemRUrVuzqpQC7AQEFAABoki677LKsWLEi1dXVufzyy3PMMcekQ4cOSZL3vve9u3h1QHMjoAAAAE3SvffemyT5+Mc/ngsvvHCnvMekSZMyadKknTI30LS4BwoAANAkLV26NEnSq1evXbwSYHcgoAAAAE3S+vXrkyQtW7bcxSsBdgcCCtAsjRkzpnIX/iR55ZVXcskll+Swww5Lhw4d0rFjxxx77LH54Q9/uM051q9fnzvuuCNf+MIX0q9fv+y7775p2bJl3vWud+VDH/pQxowZs103rbv//vtz2mmnpUePHmnbtm3atWuX7t27Z8CAARk9enTuv//+eo975ZVXcvnll2fgwIGV9+7UqVMOPfTQDBs2LDfccEOWL1/+1n5BANBETZo0aYvv+CS59NJLK69t/kScDRs25P7778/o0aMzaNCg7LfffmnZsmX22Wef/O3f/m1Gjx6d559/vsH3Kz2FB9h9uAcK0OwtWrQoH/3oR7Nw4cLKa6tWrcr06dMzffr0TJkyJZMnT0519Zb/SzznnHNy8803bzXfn//858yePTuzZ8/Od77zndx+++0ZNGhQve/9b//2bxk7duxWrz/33HN57rnn8n//93+ZNGnSViFm3rx5+chHPpIXX3xxi9dXrFiRFStWZN68eZkyZUreeOONfOELX9ju3wUA7E7+4z/+I5deeulWr7/66qt58skn8+STT+aGG27I//zP/2TYsGG7YIVAUyKgAM3epz71qSxatCjnnXdePvGJT2TvvffO3Llzc+WVV+aZZ57Jz372s3Tu3Dn/+Z//ucVxtbW1OeiggzJs2LD0798/73nPe1JdXZ3nnnsu9957b2666aa89NJLGTZsWJ566qnsv//+Wxx/5513VuLJBz/4wZx//vnp06dP9t5777z66quZP39+7rnnnsycOXOrNX/mM5/Jiy++mJYtW+bss8/OiSeemHe/+93ZsGFDXnzxxcyePTs///nPd94vDQAaqY9//OPp27dvkuQDH/hAkuT888/P5z//+cqYfffdN8nG7/LOnTtn2LBhGThwYA466KC0adMmL7zwQh555JF873vfy2uvvZZPf/rT+fWvf50+ffq88x8IaDKq6urq6nb1IgB2tDFjxmzxL04/+tGPctppp20xZuXKlTn66KPz5JNPpkWLFnniiScqfxBLkoULF+aggw7a4hThzf3mN7/Jhz/84bz22mu56KKL8o1vfGOL/aeffnr++7//O+9973vz1FNPVR6r+Nf+/Oc/p2PHjpWff//736dnz55JknHjxm3zDJO6urq88sorlT8kAsDuZtN39CWXXJIxY8ZstX/x4sU58MADt3mPlCVLlmTAgAFZunRp/vmf/zn//d//vdWYESNG5Oabb8573/veLF68eKv93bt3z3PPPZczzjjD03qgmXMPFKDZGzp06FbxJEn23HPPjB8/PsnGa6RvvPHGLfb37Nlzm/Ek2fivXp/73OeSJFOmTNlq/x/+8IckyRFHHLHNeJJki3iy+XFJcswxx2zzuKqqKvEEABrQvXv3Bm8w27Vr11xwwQVJkv/93/+Nf1sGGuISHqDZO/PMM7e5r3///jnssMPy9NNP5957721wnpdffjl//vOfs3bt2sofsPbZZ58kyW9/+9u8/vrrW/whrXPnzkmSGTNmZOHChZWzSko2HZdsvFHeddddt13HAQAN+8tf/pKXXnopq1evrnyXt2vXrrJv0aJFOeigg3blEoFGTEABmr1+/fo1uL9///55+umn8+yzz2b9+vVp1apVZd9vfvObjB07NnffffcWZ4b8tQ0bNuTll1/e4j4op59+en7wgx/kpZdeyvvf//7U1NTkYx/7WI4++ui8733v2+ZcPXr0yNFHH52HHnooY8eOzS9+8Yv84z/+Y4499tgMGDCg8gc9AKDsueeeyzXXXJM77rgjzz33XINjV6xYIaAA2+QSHqDZ++ubu/61Aw44IMnGe4q8/PLLldcnTpyYI444It///vcbjCebrFmzZoufjz/++HznO99J27Zts3bt2txyyy357Gc/m4MPPjhdu3bNeeedlyeffLLeuSZPnpyBAwcm2Xh2yze+8Y0cf/zx2WeffTJ48ODceOONWbt2bXFNALA7u/vuu3PooYfmO9/5TjGeJFt/lwNsTkABmr2G7mOSpN7rnefPn5/zzjsvtbW12X///XP11Vfnsccey0svvZT169enrq4udXV1mThxYoPz/Mu//EsWL16csWPHZsiQIdl7772TJEuXLs1//dd/5fDDD89FF1201XEHHnhgHnnkkdx77735/Oc/n8MOOyxVVVV5/fXXM2PGjJx//vl5//vfn2eeeebN/joAYLfw0ksv5dOf/nRWr16dDh06ZMyYMZk5c2aWL1+edevWVb7L77vvvsox7oECNMQlPECz98c//jHdunXb5v7ly5cn2fKmrJMmTUptbW322GOPPPjgg9t8rOHmZ6xsy/77759Ro0Zl1KhR2bBhQ5544onceuut+e53v5tXXnkll19+efr165eampqtjj3++ONz/PHHJ9n4B8F7770348ePz/3335+FCxfmU5/6VB5//PHiGgBgd/PTn/40r7zySpLk1ltvzUc/+tF6x23PdzlA4gwUYDfw6KOPbtf+gw8+uHL/k6effjpJ8jd/8zfbjCdJMmfOnDe1lhYtWuSII47IZZddtsW/eP3kJz8pHvuud70rn/rUp3Lffffl5JNPTpI88cQTefbZZ9/UGgBgd7Dpu7xjx47bjCfJm/8uB3ZfAgrQ7N18883b3Ddnzpw89dRTSZKPfOQjlddra2uTJKtXr97msX/4wx9y++23v+V1HXHEEZUzXlasWPGmjt10VspbORYAdgebvsvXrVuXDRs21Dtm9erV+cEPfvBOLgtowgQUoNn73//933rP8HjttddyzjnnJNl4Zsi5555b2XfwwQcnSZ555pnMmjVrq2NXr16dT3/60w3ebO6WW25pcP+cOXMqpw336NGj8voTTzyRJ554YpvH1dXVVR65XFVVle7du29zLADsrjZ9l69atSo/+9nPttr/xhtv5HOf+1xefPHFd3ppQBPlHihAs9e3b998+tOfzvTp0/OJT3wie+21V+bOnZsrr7wyv/vd75JsvNnrBz/4wcoxn/nMZzJu3Lhs2LAhQ4YMyYUXXpgPf/jDadOmTR577LGMHTs2zz77bAYNGpRf/epX9b7vV77ylZx33nmpqanJMccck169eqV9+/Z56aWX8vDDD2fcuHFJkj322CNnn3125bgnnngiZ555Zvr165d/+Id/yBFHHJF3v/vdef3117No0aJ8//vfzz333JMkqampSefOnXfWrw4AmqxTTjklX/va17Ju3bqMGDEiTzzxRD7ykY9kr732ytNPP51x48blsccea/C7HGBzAgrQ7P3kJz/J8ccfn+9973v53ve+t9X+f/zHf8x11123xWv9+vXLpZdemksuuSQvv/xy/v3f/32r47785S/n/e9/f4N/6HrllVdy8803b/MyojZt2uS//uu/cuSRR26179FHH23w/i1HHXXUFk8BAgD+n65du+aGG27I5z73uaxZsyZXXHFFrrjiii3GfOpTn8rZZ5+9xWW8ANviEh6g2evRo0cee+yxfO1rX0ufPn3Srl277L333jnmmGPyP//zP/nZz36W6uqte/LFF1+cqVOn5oQTTsi+++6bVq1apWvXrhk+fHh++ctf5pprrmnwfWfMmJEJEybkU5/6VD7wgQ+kU6dOqa6uzl577ZUjjjgiF1xwQX7729/m9NNP3+K4T3/603nggQfyta99LUcffXR69OiRdu3aVd7/5JNPzo9+9KNMnz49HTt23KG/KwBoTs4888w89NBD+fjHP55OnTqlZcuW6dy5c/7+7/8+t9xyS3784x9njz322NXLBJqIqjoPOweaoTFjxuTSSy9NsvGeIQAAAG+HM1AAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACjyFBwAAAKDAGSgAAAAABQIKAAAAQIGAAgAAAFAgoAAAAAAUCCgAAAAABQIKAAAAQIGAAgAAAFAgoAAAAAAUCCgAAAAABQIKAAAAQIGAAgAAAFAgoAAAAAAUCCgAQJM3adKkVFVVpaqqKosXL97Vy9mm7t27p6qqKiNGjNjVSwEA3iQBBQAAAKBAQAEAAAAoEFAAAAAACgQUAKDJevDBB1NVVZUzzzyz8lqPHj0q90PZ9N+DDz641bH33HNP/vmf/zk9evRI27Zts9dee+Vv/uZvcuGFF2bZsmUNvu+LL76Yr371qzniiCOy9957p1WrVnn3u9+dD3zgAznttNMyadKk/OUvf6mMP/bYY1NVVZXnnnsuSXLzzTdvtcZjjz12h/xOAICdo3pXLwAA4J20atWqfOYzn8ltt922xetr167N3LlzM3fu3Nxwww2ZPHlyhg4dutXxDz30UIYOHbpFIEmSP/7xj/njH/+Yp556Kj/+8Y+z33771Xs8ANA0VdXV1dXt6kUAALwVq1atyqJFi3L77bfnoosuSpL84he/SJcuXbYY16NHj7Rv3z5vvPFGPvrRj+aBBx5IVVVVTj311AwfPjw9evTI66+/ntmzZ+faa6/N888/n1atWuWRRx7JkUceWZln3bp1Oeigg/Liiy9mzz33zPnnn5/jjjsu+++/f15//fU899xzmTlzZn7+85/ne9/7XiWgLFq0KKtWrcrHPvaxvPjii6mpqclll122xRrbt2+fHj167OTfGADwVgkoAECTN2nSpMplPIsWLUr37t3rHXfttddm9OjRadmyZW6//faceOKJW415+eWXc/TRR+fpp5/OUUcdlYceeqiy7/7778/xxx+fJLnjjju2eYZJbW1tVq9enb322muL17t3757nnnsuZ5xxRiZNmvQWPikAsKu4BwoAsFt4/fXXc+211yZJvvCFL9QbT5Jk3333zdVXX50kefjhh7NgwYLKvj/84Q+V7WOOOWab71VdXb1VPAEAmjYBBQDYLcyePbtyc9hTTjmlwbGbx5GZM2dWtjt37lzZ/v73v7+DVwgANGYCCgCwW5gzZ05le+DAgVs9BWfz/zp06FAZu/lZJ0cddVQOOuigJMmoUaPSv3//XHHFFXnkkUeyfv36d+7DAADvOAEFANgtLF++/C0dt3r16sp2y5Ytc8cdd6RPnz5JkkcffTRf+9rXMmjQoOyzzz458cQT86Mf/ShvvPHGDlkzANB4eIwxALBb2DxqPPjgg3nXu961Xcftv//+W/x86KGH5je/+U3uuOOO3HHHHZk+fXoWLlyYNWvWZNq0aZk2bVquu+663HXXXVsdCwA0XQIKALBb2DyYtGrVKu9///vf8lx77LFHPv7xj+fjH/94kmTZsmW5++67873vfS+PPfZYHnvssZx77rm57bbb3u6yAYBGwiU8AECTV1VVVRxz+OGHV7Z/+ctf7tD379y5cz772c9m5syZOeKII5Ikd955Z9asWfOm1wkANE4CCgDQ5LVp06ayvW7dunrHHHXUUenYsWOS5MYbb8xf/vKXHb6Oli1bZvDgwUmS2travPLKK/Wuc1trBAAaLwEFAGjyNn+88MKFC+sd06ZNm4wePTrJxifrnHrqqVm1atU251y5cmW+853vbPHaQw89lAULFmzzmPXr12f69OlJkg4dOqRTp071rnNbawQAGq+qurq6ul29CACAt2PlypXZf//9s3bt2hxxxBG54oor0r1797RosfHfig488MC0bds2b7zxRj72sY/lvvvuS5K85z3vyXnnnZeBAwdmn332ycqVK/O73/0uDz74YKZMmZI2bdpkxYoVlfcZM2ZMvvGNb+Too4/OSSedlA9+8IPp1KlT1qxZk2eeeSY33nhjZs+enWTjY47Hjh27xTovuuiiXH755UmSK664IieeeGLat2+fJGnbtm0OPPDAnf67AgDeGgEFAGgWvvKVr+Sqq66qd98DDzyQY489NkmyZs2anHfeefnBD35QnLNHjx75/e9/X/l5zJgxufTSS4vHDR8+PD/84Q+3uLQoSZYuXZoPfvCD+fOf/7zVMYMHD86DDz5YnBsA2DUEFACgWairq8vEiRPzgx/8IE8//XReffXVyqOLNw8omzz22GOZOHFiZsyYkSVLlmTVqlXp0KFDunfvniOPPDInnnhihg4dmtatW1eOWb16daZPn5577rknM2fOzIsvvpjly5cnSd797nfnQx/6UE4//fQMGTJkm+tcuHBhrrjiikyfPj1LlizJ2rVrkwgoANDYCSgAAAAABW4iCwAAAFAgoAAAAAAUCCgAAAAABQIKAAAAQIGAAgAAAFAgoAAAAAAUCCgAAAAABQIKAAAAQIGAAgAAAFAgoAAAAAAUCCgAAAAABQIKAAAAQIGAAgAAAFAgoAAAAAAUCCgAAAAABQIKAAAAQIGAAgAAAFAgoAAAAAAUCCgAAAAABQIKAAAAQIGAAgAAAFAgoAAAAAAUCCgAAAAABQIKAAAAQMH/D9xjK1de6DdSAAAAAElFTkSuQmCC"/>


```python
# 실습 : 중첩 조건문 활용하기 (123쪽)

## 1. 연비 등급 변수 만들기
```


```python
# total 기준으로 A, B, C 등급 부여
mpg['grade'] = np.where(mpg['total'] >= 30, 'A', 
               np.where(mpg['total'] >= 20, 'B', 'C'))

# 데이터 확인
mpg.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>category</th>
      <th>total</th>
      <th>test</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>18</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
      <td>23.5</td>
      <td>pass</td>
      <td>B</td>
    </tr>
    <tr>
      <th>1</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
      <td>25.0</td>
      <td>pass</td>
      <td>B</td>
    </tr>
    <tr>
      <th>2</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>20</td>
      <td>31</td>
      <td>p</td>
      <td>compact</td>
      <td>25.5</td>
      <td>pass</td>
      <td>B</td>
    </tr>
    <tr>
      <th>3</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(av)</td>
      <td>f</td>
      <td>21</td>
      <td>30</td>
      <td>p</td>
      <td>compact</td>
      <td>25.5</td>
      <td>pass</td>
      <td>B</td>
    </tr>
    <tr>
      <th>4</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>compact</td>
      <td>21.0</td>
      <td>pass</td>
      <td>B</td>
    </tr>
  </tbody>
</table>
</div>



```python
## 2. 빈도표와 막대 그래프로 연비 등급 살펴보기

count_grade = mpg['grade'].value_counts()
count_grade
```

<pre>
grade
B    118
C    106
A     10
Name: count, dtype: int64
</pre>

```python
count_grade.plot.bar(rot = 0)
```

<pre>
<Axes: xlabel='grade'>
</pre>
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABFAAAANhCAYAAADABk+6AAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjcuMiwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8pXeV/AAAACXBIWXMAAB7CAAAewgFu0HU+AABMkklEQVR4nO3de5TXZaHv8c8gchFUQtFEUNBEwGNuExAPGtpFEy22lkZbU4zSbEdiinX2Li8nrTQVjS5GYJop2cXLMZS8gzcOouQlQQUlQUkkReXuwJw/WPwOyDDPqMDMwOu1Fms9M9/n9/yen6t+S95+L1U1NTU1AQAAAGC9mjX0BgAAAAAaOwEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKmjf0BrYUS5cuzVNPPZUk6dChQ5o3948eAAAANrTq6uq89tprSZJ99903rVq12iDr+lv8JvLUU0+lT58+Db0NAAAA2GJMnjw5vXv33iBruYQHAAAAoMAZKJtIhw4dKuPJkydnl112acDdAAAAwOZp7ty5lStA1vy7+AcloGwia97zZJdddkmnTp0acDcAAACw+duQ9x91CQ8AAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABRs1IAyb968/OUvf8m5556bI488MjvuuGOqqqpSVVWVwYMH12uNpUuX5tZbb83QoUNz4IEHpn379tl6663Tvn37HHTQQTn//PMzd+7ceu9p8eLF+clPfpI+ffqkffv2adu2bXr06JGzzz47L7300vv8pAAAAMDmrPnGXHznnXf+QK9/8sknc/DBB+ftt99e59gbb7yRSZMmZdKkSbn88sszevToHH/88XWuN3PmzBx11FF59tln1/r99OnTM3369IwePTo33HBDBgwY8IH2DQAAAGxeNtklPJ07d87hhx/+nl7z1ltvVeJJv3798qMf/Sh33XVXHn/88fz1r3/Naaedlq222ipvv/12/uM//iN33HHHetdauHBhjj766Eo8+drXvpZ77rknDz/8cC666KK0bds2b775Zo477rg8+eST7/+DAgAAAJudjXoGyrnnnpvevXund+/e2XnnnTNr1qx07dq13q9v1qxZjj/++Jx33nnp2bPnOscPP/zwHHnkkTnmmGOyYsWKDB06NM8//3yqqqrWmXvppZdm+vTpSZJLLrkkw4cPrxw76KCDcthhh+XjH/94Fi9enGHDhuXee+99H58YAAAA2BxV1dTU1GyqN1szoJx88sm55pprNsi6X/jCF/LnP/85SfL4449n//33X+v4O++8k5122ikLFixIjx498vTTT6dZs3VPvvn617+eX/3qV0mSKVOm5IADDtgg+0uSOXPmpHPnzkmS2bNnp1OnThtsbQAAAGCVjfX3783iKTyHHXZYZTxz5sx1jt9///1ZsGBBklXhprZ4kmStG9vedNNNG3SPAAAAQNO1WQSUZcuWVca1xZEHHnigMu7fv/961+nVq1fatGmTJHnwwQc34A4BAACApmyzCCgTJkyojLt3777O8WnTptV5fLXmzZtnzz33XOc1AAAAwJZto95EdlN44oknMm7cuCTJPvvsU+vNZmfPnp0kadOmTdq1a1fnep07d86TTz6Z1157LcuWLUvLli3rtY85c+bUeXzu3Ln1WgcAAABofJp0QFm2bFm++tWvZsWKFUmSH/7wh7XOW/0o5LZt2xbXXH0JT7Lq0cf1DSirb1ADAAAAbH6a9CU83/zmNzNlypQkq24O+7nPfa7WeUuXLk2StGjRorjmmsFkyZIlG2CXAAAAQFPXZM9A+dGPfpTRo0cnSQ444ID8/Oc/X+/cVq1aJUmWL19eXHfNG9K2bt263vtZfZnQ+sydOzd9+vSp93oAAABA49EkA8qvfvWr/Nd//VeSZO+9984dd9yx1qU377btttsmWXVJTsmiRYsq4/pc8rPahnquNAAAAND4NLlLeMaOHZtvfOMbSZLdd989d999dzp06FDna1bHjUWLFmXBggV1zl19JkmHDh3qff8TAAAAYPPWpALK//k//ycnnXRSVq5cmV122SX33HNPvc78WPPJPNOnT1/vvOrq6sycOTNJ0qNHjw++YQAAAGCz0GQCyj333JPjjz8+1dXV2WGHHXLXXXdlzz33rNdrDz744Mp4woQJ6503ZcqUyiU8/fr1+2AbBgAAADYbTSKgPPzwwxk4cGCWLVuW7bbbLn/961+zzz771Pv1hx56aLbffvskybXXXpuamppa511zzTWV8THHHPOB9gwAAABsPhp9QPnb3/6Wo446KosWLUqbNm1y++2354ADDnhPa7Ro0SLf+ta3kiTTpk3LpZdeus6cRx55JGPGjEmS9O/fP7179/7gmwcAAAA2Cxv1KTwPPvhgZsyYUfl5/vz5lfGMGTPWOuMjSQYPHrzWzzNnzswRRxxRufHrhRdemO233z5PP/30et9zp512yk477bTO74cPH54bb7wxzz33XM4555zMmDEjgwYNSuvWrXPfffflhz/8Yaqrq9O6detcccUV7/mzAgAAAJuvqpr1Xc+yAQwePDjXXnttvee/eyvXXHNNTjnllPf0nuedd17OP//8Wo/NmDEjAwYMyPPPP1/r8e222y7XX399jj766Pf0nvUxZ86cdO7cOcmqJ/147DEAAABseBvr79+N/hKeDekjH/lIpk6dmosvvji9evVKu3btss0222TvvffOmWeemSeffHKjxBMAAACgaduoZ6Dw/zkDZcPr8t1xDb0FWMusHx/V0FsAAIAtnjNQAAAAABqIgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFDRv6A0AABtPl++Oa+gtwFpm/fioht4CALwvzkABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAo2akCZN29e/vKXv+Tcc8/NkUcemR133DFVVVWpqqrK4MGD3/N648ePz7HHHptOnTqlZcuW6dSpU4499tiMHz++3mssXrw4P/nJT9KnT5+0b98+bdu2TY8ePXL22WfnpZdees97AgAAADZ/zTfm4jvvvPMGWaempiZf//rXM2rUqLV+//LLL+fmm2/OzTffnFNPPTVXXXVVqqqq1rvOzJkzc9RRR+XZZ59d6/fTp0/P9OnTM3r06Nxwww0ZMGDABtk3AAAAsHnYZJfwdO7cOYcffvj7eu33vve9SjzZf//9M3bs2EyePDljx47N/vvvnyQZNWpUvv/97693jYULF+boo4+uxJOvfe1rueeee/Lwww/noosuStu2bfPmm2/muOOOy5NPPvm+9gkAAABsnjbqGSjnnntuevfund69e2fnnXfOrFmz0rVr1/e0xowZM3LJJZckSXr16pWJEyemdevWSZLevXvnc5/7XPr3758pU6bk4osvzimnnJI999xznXUuvfTSTJ8+PUlyySWXZPjw4ZVjBx10UA477LB8/OMfz+LFizNs2LDce++97/djAwAAAJuZjXoGygUXXJCjjz76A13KM2LEiFRXVydJRo4cWYknq22zzTYZOXJkkqS6ujpXXHHFOmu88847ufLKK5MkPXr0yFlnnbXOnIMOOihDhgxJktx333157LHH3veeAQAAgM1Lo34KT01NTW699dYkSffu3dO3b99a5/Xt2zd77713kuSWW25JTU3NWsfvv//+LFiwIEly8sknp1mz2j/2mje2vemmmz7g7gEAAIDNRaMOKC+++GJefvnlJEn//v3rnLv6+Jw5czJr1qy1jj3wwAPrzKtNr1690qZNmyTJgw8++H62DAAAAGyGNuo9UD6oadOmVcbdu3evc+6ax6dNm7bWvVbqu07z5s2z55575sknn1zrNfUxZ86cOo/PnTv3Pa0HAAAANB6NOqDMnj27Mu7UqVOdczt37lzr69b8uU2bNmnXrl1xnSeffDKvvfZali1blpYtW9Zrr2u+PwAAALB5adSX8Lz99tuVcdu2beucu/rSm2TVI4trW6e0RmkdAAAAYMvUqM9AWbp0aWXcokWLOueueabIkiVLal2ntEZpnbq8+6yXd5s7d2769OlT7/UAAACAxqNRB5RWrVpVxsuXL69z7rJlyyrjdz/qePU6pTVK69SldIkRAAAA0HQ16kt4tt1228q4dDnNokWLKuN3X6qzep36XJJT1zoAAADAlqlRB5Q1z+ooPeVmzUto3n1D19XrLFq0KAsWLKjXOh06dKj3DWQBAACAzVujDig9e/asjKdPn17n3DWP9+jR432tU11dnZkzZ9a6BgAAALDlatQBpWvXrunYsWOSZMKECXXOnThxYpJk1113TZcuXdY6dvDBB1fGda0zZcqUyiU8/fr1ez9bBgAAADZDjTqgVFVVZeDAgUlWnTkyadKkWudNmjSpcmbJwIEDU1VVtdbxQw89NNtvv32S5Nprr01NTU2t61xzzTWV8THHHPNBtw8AAABsJhp1QEmSYcOGpXnzVQ8LGjp06DqPFl6yZEmGDh2aJGnevHmGDRu2zhotWrTIt771rSTJtGnTcumll64z55FHHsmYMWOSJP3790/v3r035McAAAAAmrCN+hjjBx98MDNmzKj8PH/+/Mp4xowZa53xkSSDBw9eZ41u3brl7LPPzo9//ONMmTIl/fr1y3e+853sueeemTlzZi6++OJMnTo1STJ8+PDstddete5l+PDhufHGG/Pcc8/lnHPOyYwZMzJo0KC0bt069913X374wx+muro6rVu3zhVXXPGBPzsAAACw+aiqWd/1LBvA4MGDc+2119Z7/vq2snLlynzta1/L1Vdfvd7XDhkyJKNGjUqzZus/qWbGjBkZMGBAnn/++VqPb7fddrn++utz9NFH13vP9TVnzpzK04Fmz5691hOGeH+6fHdcQ28B1jLrx0c19BZgHb4raWx8VwKwsW2sv383+kt4kqRZs2YZM2ZMxo0bl4EDB6Zjx45p0aJFOnbsmIEDB+b222/P6NGj64wnSfKRj3wkU6dOzcUXX5xevXqlXbt22WabbbL33nvnzDPPzJNPPrlR4gkAAADQtG3UM1D4/5yBsuH5r6o0Nv6rKo2R70oaG9+VAGxsW/QZKAAAAAANSUABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgoEkFlOXLl2fMmDH5zGc+k1122SUtW7ZM27Zts/fee+crX/lKJk2aVK91xo8fn2OPPTadOnVKy5Yt06lTpxx77LEZP378Rv4EAAAAQFPUvKE3UF+zZ8/OUUcdlaeeemqt3y9fvjzPPfdcnnvuufzmN7/JmWeemcsuuyxVVVXrrFFTU5Ovf/3rGTVq1Fq/f/nll3PzzTfn5ptvzqmnnpqrrrqq1tcDAAAAW6YmcQZKdXX1WvHkox/9aK655po88sgjufPOO3PuueemTZs2SZIRI0bk0ksvrXWd733ve5V4sv/++2fs2LGZPHlyxo4dm/333z9JMmrUqHz/+9/fBJ8KAAAAaCqqampqahp6EyV//vOf84UvfCFJctBBB+WBBx7IVltttdacxx57LAcddFDeeeedfOhDH8q8efPSvPn/P8FmxowZ6dGjR6qrq9OrV69MnDgxrVu3rhxfvHhx+vfvnylTpqR58+aZPn169txzzw32GebMmZPOnTsnWXU2TadOnTbY2luqLt8d19BbgLXM+vFRDb0FWIfvShob35UAbGwb6+/fTeIMlIceeqgy/l//63+tE0+S5IADDsjRRx+dJHnjjTcyffr0tY6PGDEi1dXVSZKRI0euFU+SZJtttsnIkSOTrDrj5YorrtiQHwEAAABowppEQFm+fHllvMcee6x33ppnjCxbtqwyrqmpya233pok6d69e/r27Vvr6/v27Zu99947SXLLLbekCZycAwAAAGwCTSKgdOvWrTJ+4YUX1jtv5syZSZKqqqrstddeld+/+OKLefnll5Mk/fv3r/O9Vh+fM2dOZs2a9X63DAAAAGxGmkRA+dKXvpTtttsuSXLxxRdnxYoV68yZOnVqxo1bdZ33oEGDKvOTZNq0aZVx9+7d63yvNY+v+bqSOXPm1Pln7ty59V4LAAAAaFyaxGOMO3TokGuuuSYnnHBCHnroofTu3TvDhg1Lt27dsnDhwjz00EO57LLLsnz58vzbv/1bLr/88rVeP3v27Mq4dPOY1TeaeffrStZ8HQAAALB5aRIBJUmOOeaYTJkyJZdffnmuvvrqnHzyyWsd33nnnXPBBRfk1FNPrTzSeLW33367Mm7btm2d77PmaxcuXLgBdg4AAAA0dU0moLzzzju54YYbctttt9V6c9dXX301Y8eOTbdu3XLUUWs/Hm/p0qWVcYsWLep8n5YtW1bGS5Ysqff+SmerzJ07N3369Kn3egAAAEDj0SQCyqJFizJgwIBMnDgxW221Vc4555yccsop2WOPPbJ06dL83//7f/O///f/zoMPPpjPfvazGTFiRM4444zK61u1alUZr/lEn9qs+fSedz/quC4b6rnSAAAAQOPTJG4ie95552XixIlJkjFjxuTiiy9O9+7d06JFi2y33Xb59Kc/nfvuuy+HHXZYampq8u1vfztPPvlk5fXbbrttZVy6LGfRokWVcelyHwAAAGDL0OgDSk1NTX7zm98kWfU443ff+2S15s2b5wc/+EGSZOXKlZXXJGufHTJnzpw632/NS3HcGBYAAABImkBAefXVV/P6668nSfbff/865x5wwAGV8fTp0yvjnj171vr72qx5vEePHu9prwAAAMDmqdEHlObN//9tWqqrq+uc+84779T6uq5du6Zjx45JkgkTJtS5xupLhXbdddd06dLlvW4XAAAA2Aw1+oDSvn37bLfddkmSRx55pM6IsmYc6dq1a2VcVVWVgQMHJll1hsmkSZNqff2kSZMqZ6AMHDgwVVVVH3j/AAAAQNPX6ANKs2bNKo8lfuWVV3LRRRfVOu+NN97Id77zncrPRx999FrHhw0bVjkrZejQoes8onjJkiUZOnRoklVnrwwbNmxDfQQAAACgiWv0ASVJzj333GyzzTZJkvPPPz+f+9zn8uc//zlTp07NI488khEjRuTf/u3f8swzzyRJPvnJT+bwww9fa41u3brl7LPPTpJMmTIl/fr1y4033pgpU6bkxhtvTL9+/TJlypQkyfDhw7PXXnttwk8IAAAANGbNy1MaXvfu3XPrrbfmS1/6UubPn5/bbrstt912W61zP/GJT+SPf/xjrccuuuiizJs3L1dffXWmTp2aQYMGrTNnyJAhufDCCzfo/gEAAICmrUmcgZIkn/rUpzJ9+vRcfPHFOfTQQ9OhQ4dsvfXWad26dbp27Zrjjz8+t9xyS+6+++586EMfqnWNZs2aZcyYMRk3blwGDhyYjh07pkWLFunYsWMGDhyY22+/PaNHj06zZk3mHwsAAACwCTSJM1BW22GHHXLOOefknHPO+UDrDBgwIAMGDNhAuwIAAAA2d061AAAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAAChocgFl/vz5ueSSS9KvX798+MMfTsuWLdOxY8cceOCBGT58eB555JHiGuPHj8+xxx6bTp06pWXLlunUqVOOPfbYjB8/fhN8AgAAAKCpad7QG3gv/vjHP+b000/Pv/71r7V+P3fu3MydOzeTJ0/O888/n1tuuaXW19fU1OTrX/96Ro0atdbvX3755dx88825+eabc+qpp+aqq65KVVXVxvoYAAAAQBPTZALKb3/725xyyilZuXJldtppp5x++uk5+OCD0759+/zzn//MzJkzc9ttt2Xrrbde7xrf+973KvFk//33zznnnJM999wzM2fOzCWXXJKpU6dm1KhR6dChQy688MJN9dEAAACARq5JBJRp06bl1FNPzcqVK3PIIYfktttuy/bbb7/OvKFDh2b58uW1rjFjxoxccsklSZJevXpl4sSJad26dZKkd+/e+dznPpf+/ftnypQpufjii3PKKadkzz333HgfCgAAAGgymsQ9UIYOHZply5Zlxx13zE033VRrPFmtRYsWtf5+xIgRqa6uTpKMHDmyEk9W22abbTJy5MgkSXV1da644ooNs3kAAACgyWv0AWX69Om55557kiTf/OY3s+OOO77nNWpqanLrrbcmSbp3756+ffvWOq9v377Ze++9kyS33HJLampq3ueuAQAAgM1Jow8of/zjHyvj4447rjJ+44038vzzz69zQ9navPjii3n55ZeTJP37969z7urjc+bMyaxZs97HjgEAAIDNTaO/B8qkSZOSJNtvv3169OiR66+/PpdcckmefPLJypyuXbvm5JNPzllnnZW2bduus8a0adMq4+7du9f5fmsenzZtWrp27Vqvfc6ZM6fO43Pnzq3XOgAAAEDj0+gDyjPPPJMk6dKlS4YOHZqf//zn68x58cUXc/755+dPf/pT/vrXv6Zjx45rHZ89e3Zl3KlTpzrfr3PnzrW+rmTN1wEAAACbl0Z/Cc/rr7+eZNW9UH7+85+nXbt2ueqqqzJv3rwsXbo0jz76aI488sgkydNPP53jjjsuK1euXGuNt99+uzKu7QyVNbVp06YyXrhw4Yb6GAAAAEAT1ujPQFm0aFGSZNmyZdlqq61yxx13rHUT2F69euUvf/lLjj766Nxxxx15+OGHc9NNN+ULX/hCZc7SpUsr4/U9pWe1li1bVsZLliyp9z5LZ6vMnTs3ffr0qfd6AAAAQOPR6ANKq1atKhHluOOOq/UJOs2aNctPfvKT3HHHHUmSsWPHrhVQWrVqVRkvX768zvdbtmxZZfzuRx3XpXRpEAAAANB0NfpLeLbddtvKePWlOrXZZ599suuuuyZJHn300fWuUbosZ3WsScqX+wAAAABbhkYfUNa8OWt9bwA7b968tX6/5utKT8tZ81IcN4YFAAAAkiYQUPbZZ5/KeMWKFXXOXX28efO1r0zq2bNnZTx9+vQ611jzeI8ePeq9TwAAAGDz1egDysc//vHKeObMmXXOfeGFF5KkcinPal27dq082njChAl1rjFx4sTKGl26dHmv2wUAAAA2Q40+oHzuc5/L1ltvnSS56aab1jtvwoQJ+de//pUkOeSQQ9Y6VlVVlYEDByZZdYbJpEmTal1j0qRJlTNQBg4cmKqqqg+8fwAAAKDpa/QBZYcddshXv/rVJMldd92V3//+9+vMefvttzNs2LDKz6eddto6c4YNG1a5tGfo0KHrPKJ4yZIlGTp0aJJVlwCtuR4AAACwZWv0ASVJLrjgguy2225Jki9/+csZOnRo7rvvvjz22GO55ppr0qdPn/ztb39Lkpx++unp3bv3Omt069YtZ599dpJkypQp6devX2688cZMmTIlN954Y/r165cpU6YkSYYPH5699tpr03w4AAAAoNFrXp7S8Dp06JDx48fnc5/7XGbMmJGf/exn+dnPfrbOvK985Su58sor17vORRddlHnz5uXqq6/O1KlTM2jQoHXmDBkyJBdeeOEG3T8AAADQtDWJM1CSVU/E+dvf/paf/OQnOfDAA9O+ffu0aNEinTp1yhe/+MXce++9GTNmTOV+KbVp1qxZxowZk3HjxmXgwIHp2LFjWrRokY4dO2bgwIG5/fbbM3r06DRr1mT+sQAAAACbQJM4A2W1Nm3a5Oyzz65civN+DRgwIAMGDNhAuwIAAAA2d061AAAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKmnRAOeecc1JVVVX5c//99xdfM378+Bx77LHp1KlTWrZsmU6dOuXYY4/N+PHjN/6GAQAAgCapyQaUJ554IiNGjKj3/Jqampx22mk58sgjc/PNN+fll1/O8uXL8/LLL+fmm2/OkUcemdNOOy01NTUbcdcAAABAU9QkA8rKlSvzta99LdXV1dlpp53q9Zrvfe97GTVqVJJk//33z9ixYzN58uSMHTs2+++/f5Jk1KhR+f73v7/R9g0AAAA0TU0yoPz0pz/No48+mu7du2fIkCHF+TNmzMgll1ySJOnVq1ceeuihDBo0KL17986gQYPy4IMPplevXkmSiy++ODNnztyo+wcAAACaliYXUGbPnl05S+SXv/xlWrRoUXzNiBEjUl1dnSQZOXJkWrduvdbxbbbZJiNHjkySVFdX54orrtiwmwYAAACatCYXUL7xjW9k4cKFOfnkk3PooYcW59fU1OTWW29NknTv3j19+/atdV7fvn2z9957J0luueUW90IBAAAAKppUQPnDH/6Qv/zlL2nfvn1+8pOf1Os1L774Yl5++eUkSf/+/eucu/r4nDlzMmvWrA+0VwAAAGDz0byhN1BfCxYsyBlnnJFk1X1KOnToUK/XTZs2rTLu3r17nXPXPD5t2rR07dq13vubM2dOncfnzp1b77UAAACAxqXJBJRzzjkn//znP/M//+f/rNeNY1ebPXt2ZdypU6c653bu3LnW19XHmq8FAAAANi9N4hKeBx98MKNHj07z5s1z1VVXpaqqqt6vffvttyvjtm3b1jm3TZs2lfHChQvf+0YBAACAzVKjPwNl+fLlOfXUU1NTU5Mzzzwz++6773t6/dKlSyvj0hN7WrZsWRkvWbLkPb1P6YyVuXPnpk+fPu9pTQAAAKBxaPQB5Yc//GGmTZuW3XbbLeedd957fn2rVq0q4+XLl9c5d9myZZXxux91XFK6PAgAAABouhr1JTzTp0/Pj370oyTJyJEj17rEpr623Xbbyrh0Wc6iRYsq49LlPgAAAMCWo1GfgTJixIgsX748e+yxRxYvXpzf//7368x5+umnK+N77703//znP5Mkn/3sZ9OmTZu1zgwpPSlnzctw3BQWAAAAWK1RB5TVl9S88MIL+dKXvlSc/4Mf/KAyfvHFF9OmTZv07Nmz8rvp06fX+fo1j/fo0eO9bhcAAADYTDXqS3g2hK5du6Zjx45JkgkTJtQ5d+LEiUmSXXfdNV26dNnYWwMAAACaiEYdUK655prU1NTU+WfNG8ved999ld+vDiBVVVUZOHBgklVnmEyaNKnW95o0aVLlDJSBAwe+p0clAwAAAJu3Rh1QNpRhw4alefNVVysNHTp0nUcUL1myJEOHDk2SNG/ePMOGDdvUWwQAAAAasS0ioHTr1i1nn312kmTKlCnp169fbrzxxkyZMiU33nhj+vXrlylTpiRJhg8fnr322qshtwsAAAA0Mo36JrIb0kUXXZR58+bl6quvztSpUzNo0KB15gwZMiQXXnhhA+wOAAAAaMy2iDNQkqRZs2YZM2ZMxo0bl4EDB6Zjx45p0aJFOnbsmIEDB+b222/P6NGj06zZFvOPBAAAAKinJn8Gyvnnn5/zzz+/3vMHDBiQAQMGbLwNAQAAAJsdp1sAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFDSJgPL444/nhz/8YY488sh07tw5LVu2TNu2bdOtW7cMHjw4DzzwwHtab/z48Tn22GPTqVOntGzZMp06dcqxxx6b8ePHb6RPAAAAADRlzRt6AyX9+/fPxIkT1/n98uXL8/zzz+f555/Ptddemy9/+csZPXp0WrRosd61ampq8vWvfz2jRo1a6/cvv/xybr755tx888059dRTc9VVV6WqqmqDfxYAAACgaWr0Z6C8/PLLSZKOHTvmjDPOyJ/+9KdMnjw5jzzySC6//PLsuuuuSZLrrrsugwcPrnOt733ve5V4sv/++2fs2LGZPHlyxo4dm/333z9JMmrUqHz/+9/feB8IAAAAaHKqampqahp6E3U5+uijc9JJJ+Xzn/98ttpqq3WOz58/P/369ctzzz2XJJk4cWIOOeSQdebNmDEjPXr0SHV1dXr16pWJEyemdevWleOLFy9O//79M2XKlDRv3jzTp0/PnnvuucE+x5w5c9K5c+ckyezZs9OpU6cNtvaWqst3xzX0FmAts358VENvAdbhu5LGxnclABvbxvr7d6M/A+Uvf/lLjj/++FrjSZLsuOOOueyyyyo//+lPf6p13ogRI1JdXZ0kGTly5FrxJEm22WabjBw5MklSXV2dK664YgPsHgAAANgcNPqAUh+HHnpoZTxz5sx1jtfU1OTWW29NknTv3j19+/atdZ2+fftm7733TpLccsstaeQn5wAAAACbyGYRUJYvX14ZN2u27kd68cUXK/dS6d+/f51rrT4+Z86czJo1a8NtEgAAAGiyGv1TeOpjwoQJlXH37t3XOT5t2rQ6j69pzePTpk1L165d67WHOXPm1Hl87ty59VoHAAAAaHyafEBZuXJlfvzjH1d+Pv7449eZM3v27Mq4dPOY1TeaeffrStZ8HQAAALB5afKX8IwYMSKTJ09OkhxzzDHp1avXOnPefvvtyrht27Z1rtemTZvKeOHChRtolwAAAEBT1qTPQJkwYUK++93vJkl22mmn/PKXv6x13tKlSyvjFi1a1Llmy5YtK+MlS5bUey+ls1Xmzp2bPn361Hs9AAAAoPFosgHl73//e4455phUV1enZcuW+cMf/pCdd9651rmtWrWqjNe84Wxtli1bVhm/+1HHddlQz5UGAAAAGp8meQnP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Wzf09mCDElBgC7FmQDnvvPNy/vnn1zrvmWeeSa9evbJkyZJst912mT9/frbeeutNuFOAhnPdddflpJNOSpJ06NAhN954Y51n7z311FMZNmxY/vWvfwkowBbpD3/4Q774xS8mScaMGZMhQ4YkScaOHZtBgwY15NZgg3MPFGAtPXv2rJyG/tZbb2XatGkNvCOATeOVV17J6aefniTZZptt6nXp47777pu77rorZ5999qbYIkCjc+211yZZ9e+QX/nKV9KzZ88kyW9/+9uG3BZsFAIKsI4uXbpUxkuXLm24jQBsQiNGjMiiRYuSJBdccEHlLwElzZo1y4knnrgxtwbQKM2bNy933nlnklS+B0844YQkyZ133plXX321wfYGG4OAAqxj1qxZlfFuu+3WcBsB2ERqamoq/xW1TZs2OfXUUxt4RwCN3/XXX5/q6upUVVVVwskJJ5yQqqqqrFixItdff30D7xA2LAEFWMv06dMzbty4JEnv3r3z4Q9/uIF3BLDxPfPMM3nttdeSJIcccki22267Bt4RQOO3Ojwfcsghlf/otvvuu+fggw9O4jIeNj/NG3oDwKY3b968PP3005Wfa2pqsmDBgspTeFbfQPaKK65ouE0CbEJPPPFEZfyxj32sAXcC0DQ89dRTle/Od1/GeOKJJ+aBBx7IE088kaeeeir77rtvQ2wRNjgBBbZAv/zlL/PLX/6y1mPNmjXLaaedlmHDhqV79+6beGcADWP+/PmV8c4779yAOwFoGlaffdKyZcscd9xxax07/vjj861vfSvLli3Ltddem0svvbQhtggbnEt4gLWsXLkyf/jDHzJ69OgsX768obcDsEm8/fbblXGbNm0acCcAjd+KFStyww03JEmOOuqotGvXbq3j7dq1y4ABA5IkN9xwQ1asWLGptwgbhYACW6DzzjsvNTU1a/1ZvHhxnnzyyQwfPjxvv/12Lrvsshx++OFZsmRJQ28XYKPbdtttK+PVT+IBoHZ33nln5s6dm2Tdy3dWW/37uXPn5u67795ke4ONSUABkiStW7fOvvvum0suuSS/+MUvkiQTJkzIj370owbeGcDGt+OOO1bGHrsJULfVN4dt165djjrqqFrnrHlmipvJsrkQUIB1DBkyJO3bt0+SjBkzpoF3A7Dx7bfffpXx448/3oA7AWjc3nrrrdx6661JkgULFqRly5apqqpa50+rVq2yYMGCJMktt9yy1qWS0FQJKMA6mjVrlr322itJ8sorr+T1119v4B0BbFw9e/asnIXywAMP5K233mrgHQE0Tn/4wx/e8yXeixcvzp/+9KeNtCPYdDyFB6hVdXV1ZfzOO+804E4ANr6qqqoMHjw4l156aRYtWpTRo0fn29/+dkNvC6DRWX05zi677JLLL7+8OP873/lOXnrppfz2t7/NKaecsrG3BxuVgAKsY/HixXnmmWeSJK1atVrr3gAAm6thw4blF7/4RRYvXpxzzz03AwYMqNfj3FeuXJkbbrhhvTdSBNhcvPjii3nwwQeTJJ///OczaNCg4mumTJmSyy67LBMmTMhLL72U3XbbbWNvEzYal/AA6zjvvPMqp2YeccQR2WqrrRp4RwAb36677pqf/exnSVY9iad///6ZMGFCna955plncsQRR+TSSy/dFFsEaFDXXXddampqkiRf+MIX6vWa1fNqampy3XXXbbS9waZQVbP6/wHAZu3+++/PYYcdliQ5/fTT841vfGOt40uXLs3zzz+f3/72txk/fnySVWefTJ48Ofvuu+8m3y9AQ/nBD36Qc889t/Lz4YcfnoEDB6ZHjx5p165dXn/99Tz33HMZN25cxo8fnxUrVmS//fbL3/72t4bbNMAmsNdee2XGjBnZaaedMnfu3DRrVv7v8TU1Ndltt90yZ86c7L333pk+ffom2ClsHAIKbCHWDCj10aFDh/zud7/L4YcfvhF3BdA43XTTTTnrrLMya9as4tx99tknl19+ue9LYLP20EMP5eCDD06SnHbaabnqqqvq/dozzjgjP/3pT5MkkyZNyoEHHrhR9ggbm0t4gCRJixYt8uEPfzif/OQnc9lll+XZZ5/1lwFgi3Xsscfm2WefzfXXX58TTzwxe++9dz70oQ+lefPmad++fT72sY/lG9/4Ru6555489dRTvi+Bzd7qm8cmq+5/8l6sOX/NdaCpcQYKAAAAQIEzUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAANoH7778/VVVVqaqqyv3339/Q2wEA3iMBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAGp358+dn+PDh6datW1q3bp2dd945n/70p3PzzTcnSa655prKE21mzZq11mu7dOmSqqqqDB48OEny2GOPZfDgwenatWtatmyZqqqqtea/8MILueyyy/LZz342Xbp0SevWrdO6devsvvvu+eIXv5jx48fXa89LlizJRRddlP322y9t2rTJDjvskH79+uXXv/51Vq5cWe/PXlNTkz/96U/5/Oc/n86dO6dVq1b50Ic+lD59+uQHP/hBFixYUO+1AIANp6qmpqamoTcBALDaE088kU9/+tN57bXXaj1+6qmn5qCDDsopp5ySJHnxxRfTpUuXyvEuXbrkH//4R04++eT07ds3Q4cOTXV19VprrP7XnxdffDF77LFHcU8nnnhifvOb36R58+a1Hn/llVfyyU9+MtOnT6/1+Gc+85mceeaZOeKII5Ik9913Xw499NB15r322ms55phj8tBDD613LzvvvHNuvfXWHHjggcV9AwAbTu3/FgAA0ADeeOONfOYzn6nEkxNOOCEnnnhiOnTokBkzZuTKK6/MqFGj8sQTTxTXevTRR/O73/0unTt3ztlnn50DDjggK1asyAMPPFCZs2LFirRo0SJHHHFEPv3pT6dnz55p3759Xn/99Tz33HP5+c9/nr///e/53e9+lz322CMXXHDBOu9TXV2do48+uhJPDj/88Jx++unp3LlzXnrppfziF7/I+PHj869//avO/S5atCj9+/fPtGnT0qJFi5xyyikZMGBAOnfunEWLFmXixIm5/PLL8+qrr+bII4/M1KlTs/vuu7+Xf7wAwAfgDBQAoNE444wz8tOf/jRJcumll+ass85a6/iKFSvy+c9/Prfeemvld+s7AyVJ9t1330ycODHt2rWr9f0WLVqUt956K7vsskutx2tqavKVr3wl11xzTdq0aZOXX34522+//VpzRo4cmW9961tJVp0d86tf/WqddYYMGZKrr7668nNtZ6AMHTo0P/vZz7L99tvn7rvvTq9evdZZ5x//+EcOOuigzJ07NyeeeGKuu+66WvcNAGx4AgoA0CgsXbo0H/7wh/Pmm2/mYx/7WKZMmbLO/UqS5NVXX02XLl2ydOnSJHUHlIkTJ+aQQw75QPt6/fXXs9NOO2XFihWVe5OsqWfPnpk2bVp23nnnvPDCC9lmm23WWWPhwoXZY489KmfWvDugzJ8/P507d87SpUtz5ZVXVoJMbX75y1/mG9/4RrbeeussWLCg1vcDADY8N5EFABqFxx57LG+++WaS5KSTTqo1niSr7gGy+l4idencufN7jifvvPNO5syZk2nTpuXpp5/O008/nVdeeSU77LBDkqxz6dArr7ySadOmJUmOP/749caMtm3b5vjjj1/v+/71r3+tBKG65iXJxz/+8cpeH3vssfp9MADgA3MPFACgUXj66acr4wMOOKDOub169VrrMp7afPSjH63X+77zzjsZNWpUrrvuukydOjXLly9f79z58+ev9fNTTz1VGffu3bvO9+nTp09+/vOf13psypQplfH6LieqzT//+c96zwUAPhgBBQBoFN54443KeKeddqpzbocOHYrrfehDHyrOef3113P44YfX+0yOJUuWrPXze9nzzjvvvN5j8+bNq9f7v9vixYvf1+sAgPdOQAEANktbbbVVcc4ZZ5xRiSf//u//nq985Sv56Ec/mp122imtWrWqXEa02267Zfbs2Xn3rePW/Hl9lxzVNvfdVqxYkSRp0aLFe7osp1OnTvWeCwB8MAIKANAorHnGyLx589KtW7f1zl19M9YP4q233sqNN96YJPmP//iPXH/99eudu+aZJmtq3759Zfzqq6/W+X51nWWy+h4ry5cvzw477PCeLuMBADYNN5EFABqFffbZpzJe854gtSkdr4/nn38+77zzTpJk0KBB65337LPPZuHChbUe23fffSvjRx99tM73q+v4/vvvXxnfeeedda4DADQMAQUAaBR69eqV7bffPkly3XXXrfeSl1dffTV//etfP/D7VVdXV8Z13UvkqquuWu+xjh07pkePHkmSP/7xj+vcI2W1RYsW5Q9/+MN61znyyCOz9dZbJ0lGjBix1t4AgMZBQAEAGoVWrVrlpJNOSpI8/vjjufzyy9eZs3Llypx22mmVR/5+EB/5yEcq9y357W9/W+ucv/zlLxk5cmSd65x++ulJVj0R56yzzqp1zplnnlnnJTy77rprTjnllCSrHpV82mmn1RlR5s2bl9GjR9e5LwBgw6qqqeuOZgAAm9Drr7+effbZp/J43hNOOCFf/vKX06FDh8yYMSNXXnllHn744fTp0yeTJ09OksyaNSu77757ZY0uXbrkH//4R04++eRcc801db7f0UcfnXHjxiVJjjjiiJx22mnZbbfdMm/evPz5z3/ONddckz322CMLFizIa6+9Vuua1dXV6dOnT6ZOnZok+cxnPpOvf/3r6dy5c2bPnp1f/OIXufPOO9O7d+/KZTz33XdfDj300LXWWbhwYQ466KDK45x79uyZU089NQcccEDatm2bBQsW5O9//3vuvvvu3H777dl33303yKVMAED9CCgAQKPyxBNP5NOf/vR6bxQ7ePDgHHLIIRkyZEiSVWd+rPmI4PcSUGbPnp2DDz44L730Uq3Hd9ttt9xxxx0ZMGBAnWu+8sor+cQnPpFnn3221nUOP/zwnHXWWTniiCOS1B5QklUB6YQTTsj48ePr3HeSHHbYYbn33nuL8wCADcMlPABAo7LffvvlmWeeyVlnnZW99torLVu2zI477pjDDjssN9xwQ37zm9/krbfeqsxffd+U96Nz5855/PHHM3z48HTr1i0tW7bM9ttvn/322y/nnXde/va3v6Vnz57FdTp27JipU6fmwgsvzP/4H/8jrVu3Trt27dK3b9/84he/yB133JEWLVoU12nfvn3uuOOO3HPPPTnllFOy1157pW3btmnevHnat2+f3r175z//8z9z++2356677nrfnxsAeO+cgQIANDlf/epXM2bMmHTq1CmzZ89u6O0AAFsAZ6AAAE3KkiVLcuuttyZJ+vbt28C7AQC2FAIKANCozJw5c72PMF6xYkVOP/30zJ8/P0ly8sknb8qtAQBbMJfwAACNyuDBgzN58uQMGjQoBx54YHbaaacsWbIkTz75ZH7961/n8ccfT5J88pOfzF133VV5FDEAwMbUvKE3AADwbtOmTct555233uP9+vXLjTfeKJ4AAJuMM1AAgEbl2WefzZ///Ofcdddd+cc//pHXXnst77zzTnbYYYf06tUrX/ziFzNo0KA0a+ZKZABg0xFQAAAAAAr8pxsAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoOD/AYyOJjtklvhYAAAAAElFTkSuQmCC"/>


```python
# 알파벳 순으로 막대 정렬하기

count_grade = mpg['grade'].value_counts().sort_index()
count_grade
```

<pre>
grade
A     10
B    118
C    106
Name: count, dtype: int64
</pre>

```python
count_grade.plot.bar(rot = 0)
```

<pre>
<Axes: xlabel='grade'>
</pre>
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABFAAAANhCAYAAADABk+6AAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjcuMiwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8pXeV/AAAACXBIWXMAAB7CAAAewgFu0HU+AABMmklEQVR4nO3de5TXZaHv8c8gchFUQtFEUNBEwGNtExAPGtpFEy22lkZbU5TytiMxxTp7l5eTVpqKRhcjMM2U7OLlGEqaKajJQRRvCSooCUoiKSp3B+b8weJ3QIZ5RgVmBl6vtVjrO/N9fs/v+bFaE/P2+X6/VTU1NTUBAAAAYL2aNfQCAAAAABo7AQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAqaN/QCthRLly7NU089lSTp0KFDmjf3Vw8AAAAbWnV1dV577bUkyb777ptWrVptkHn9Fr+JPPXUU+nTp09DLwMAAAC2GJMnT07v3r03yFwu4QEAAAAosANlE+nQoUPlePLkydlll10acDUAAACweZo7d27lCpA1fxf/oASUTWTNe57ssssu6dSpUwOuBgAAADZ/G/L+oy7hAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAgo0aUObNm5c//elPOf/883PEEUdkxx13TFVVVaqqqjJ48OB6zbF06dLcfvvtGTp0aA444IC0b98+W2+9ddq3b58DDzwwF154YebOnVvvNS1evDg/+tGP0qdPn7Rv3z5t27ZNjx49cu655+all156n58UAAAA2Jw135iT77zzzh/o9U8++WQOOuigvP322+uce+ONNzJp0qRMmjQpV155ZUaPHp3jjjuuzvlmzpyZI488Ms8+++xa358+fXqmT5+e0aNH56abbsqAAQM+0LoBAACAzcsmu4Snc+fOOeyww97Ta956661KPOnXr19+8IMf5J577sljjz2WP//5zznttNOy1VZb5e23385//Md/5K677lrvXAsXLsxRRx1ViSdf+9rXcu+99+Zvf/tbLrnkkrRt2zZvvvlmjj322Dz55JPv/4MCAAAAm52NugPl/PPPT+/evdO7d+/svPPOmTVrVrp27Vrv1zdr1izHHXdcLrjggvTs2XOd84cddliOOOKIHH300VmxYkWGDh2a559/PlVVVeuMvfzyyzN9+vQkyWWXXZbhw4dXzh144IE59NBD84lPfCKLFy/OsGHD8te//vV9fGIAAABgc1RVU1NTs6nebM2ActJJJ+W6667bIPN+8YtfzB//+MckyWOPPZb99ttvrfPvvPNOdtpppyxYsCA9evTI008/nWbN1t18c/rpp+cXv/hFkmTKlCnZf//9N8j6kmTOnDnp3LlzkmT27Nnp1KnTBpsbAAAAWGVj/f69WTyF59BDD60cz5w5c53z999/fxYsWJBkVbipLZ4kWevGtrfccssGXSMAAADQdG0WAWXZsmWV49riyAMPPFA57t+//3rn6dWrV9q0aZMkefDBBzfgCgEAAICmbLMIKBMmTKgcd+/efZ3z06ZNq/P8as2bN8+ee+65zmsAAACALdtGvYnspvDEE09k3LhxSZJ99tmn1pvNzp49O0nSpk2btGvXrs75OnfunCeffDKvvfZali1blpYtW9ZrHXPmzKnz/Ny5c+s1DwAAAND4NOmAsmzZsnz1q1/NihUrkiTf//73ax23+lHIbdu2Lc65+hKeZNWjj+sbUFbfoAYAAADY/DTpS3i+/vWvZ8qUKUlW3Rz285//fK3jli5dmiRp0aJFcc41g8mSJUs2wCoBAACApq7J7kD5wQ9+kNGjRydJ9t9///z0pz9d79hWrVolSZYvX16cd80b0rZu3bre61l9mdD6zJ07N3369Kn3fAAAAEDj0SQDyi9+8Yv813/9V5Jk7733zl133bXWpTfvtu222yZZdUlOyaJFiyrH9bnkZ7UN9VxpAAAAoPFpcpfwjB07NmeeeWaSZPfdd89f/vKXdOjQoc7XrI4bixYtyoIFC+ocu3onSYcOHep9/xMAAABg89akAsr/+T//JyeeeGJWrlyZXXbZJffee2+9dn6s+WSe6dOnr3dcdXV1Zs6cmSTp0aPHB18wAAAAsFloMgHl3nvvzXHHHZfq6urssMMOueeee7LnnnvW67UHHXRQ5XjChAnrHTdlypTKJTz9+vX7YAsGAAAANhtNIqD87W9/y8CBA7Ns2bJst912+fOf/5x99tmn3q8/5JBDsv322ydJrr/++tTU1NQ67rrrrqscH3300R9ozQAAAMDmo9EHlMcffzxHHnlkFi1alDZt2uTOO+/M/vvv/57maNGiRb7xjW8kSaZNm5bLL798nTEPP/xwxowZkyTp379/evfu/cEXDwAAAGwWNupTeB588MHMmDGj8vX8+fMrxzNmzFhrx0eSDB48eK2vZ86cmcMPP7xy49eLL74422+/fZ5++un1vudOO+2UnXbaaZ3vDx8+PDfffHOee+65nHfeeZkxY0YGDRqU1q1b57777sv3v//9VFdXp3Xr1rnqqqve82cFAAAANl9VNeu7nmUDGDx4cK6//vp6j3/3Uq677rqcfPLJ7+k9L7jgglx44YW1npsxY0YGDBiQ559/vtbz2223XW688cYcddRR7+k962POnDnp3LlzklVP+vHYYwAAANjwNtbv343+Ep4N6SMf+UimTp2aSy+9NL169Uq7du2yzTbbZO+9987ZZ5+dJ598cqPEEwAAAKBp26g7UPj/7EABoCF0+fa4hl4CrGXWD49s6CUAsJmzAwUAAACggQgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAEBB84ZeAAAAQEPp8u1xDb0EWMesHx7Z0EugFnagAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFGzWgzJs3L3/6059y/vnn54gjjsiOO+6YqqqqVFVVZfDgwe95vvHjx+eYY45Jp06d0rJly3Tq1CnHHHNMxo8fX+85Fi9enB/96Efp06dP2rdvn7Zt26ZHjx4599xz89JLL73nNQEAAACbv+Ybc/Kdd955g8xTU1OT008/PaNGjVrr+y+//HJuvfXW3HrrrTn11FNzzTXXpKqqar3zzJw5M0ceeWSeffbZtb4/ffr0TJ8+PaNHj85NN92UAQMGbJB1AwAAAJuHTXYJT+fOnXPYYYe9r9d+5zvfqcST/fbbL2PHjs3kyZMzduzY7LfffkmSUaNG5bvf/e5651i4cGGOOuqoSjz52te+lnvvvTd/+9vfcskll6Rt27Z58803c+yxx+bJJ598X+sEAAAANk8bdQfK+eefn969e6d3797ZeeedM2vWrHTt2vU9zTFjxoxcdtllSZJevXpl4sSJad26dZKkd+/e+fznP5/+/ftnypQpufTSS3PyySdnzz33XGeeyy+/PNOnT0+SXHbZZRk+fHjl3IEHHphDDz00n/jEJ7J48eIMGzYsf/3rX9/vxwYAAAA2Mxt1B8pFF12Uo4466gNdyjNixIhUV1cnSUaOHFmJJ6tts802GTlyZJKkuro6V1111TpzvPPOO7n66quTJD169Mg555yzzpgDDzwwQ4YMSZLcd999efTRR9/3mgEAAIDNS6N+Ck9NTU1uv/32JEn37t3Tt2/fWsf17ds3e++9d5LktttuS01NzVrn77///ixYsCBJctJJJ6VZs9o/9po3tr3llls+4OoBAACAzUWjDigvvvhiXn755SRJ//796xy7+vycOXMya9astc498MAD64yrTa9evdKmTZskyYMPPvh+lgwAAABshjbqPVA+qGnTplWOu3fvXufYNc9PmzZtrXut1Hee5s2bZ88998yTTz651mvqY86cOXWenzt37nuaDwAAAGg8GnVAmT17duW4U6dOdY7t3Llzra9b8+s2bdqkXbt2xXmefPLJvPbaa1m2bFlatmxZr7Wu+f4AAADA5qVRX8Lz9ttvV47btm1b59jVl94kqx5ZXNs8pTlK8wAAAABbpka9A2Xp0qWV4xYtWtQ5ds2dIkuWLKl1ntIcpXnq8u5dL+82d+7c9OnTp97zAQAAAI1How4orVq1qhwvX768zrHLli2rHL/7Ucer5ynNUZqnLqVLjAAAAICmq1FfwrPttttWjkuX0yxatKhy/O5LdVbPU59LcuqaBwAAANgyNeqAsuaujtJTbta8hObdN3RdPc+iRYuyYMGCes3ToUOHet9AFgAAANi8NeqA0rNnz8rx9OnT6xy75vkePXq8r3mqq6szc+bMWucAAAAAtlyNOqB07do1HTt2TJJMmDChzrETJ05Mkuy6667p0qXLWucOOuigynFd80yZMqVyCU+/fv3ez5IBAACAzVCjDihVVVUZOHBgklU7RyZNmlTruEmTJlV2lgwcODBVVVVrnT/kkEOy/fbbJ0muv/761NTU1DrPddddVzk++uijP+jyAQAAgM1Eow4oSTJs2LA0b77qYUFDhw5d59HCS5YsydChQ5MkzZs3z7Bhw9aZo0WLFvnGN76RJJk2bVouv/zydcY8/PDDGTNmTJKkf//+6d2794b8GAAAAEATtlEfY/zggw9mxowZla/nz59fOZ4xY8ZaOz6SZPDgwevM0a1bt5x77rn54Q9/mClTpqRfv3751re+lT333DMzZ87MpZdemqlTpyZJhg8fnr322qvWtQwfPjw333xznnvuuZx33nmZMWNGBg0alNatW+e+++7L97///VRXV6d169a56qqrPvBnBwAAADYfVTXru55lAxg8eHCuv/76eo9f31JWrlyZr33ta7n22mvX+9ohQ4Zk1KhRadZs/ZtqZsyYkQEDBuT555+v9fx2222XG2+8MUcddVS911xfc+bMqTwdaPbs2Ws9YQgANpYu3x7X0EuAtcz64ZENvQRYi5+TNEZ+Vn4wG+v370Z/CU+SNGvWLGPGjMm4ceMycODAdOzYMS1atEjHjh0zcODA3HnnnRk9enSd8SRJPvKRj2Tq1Km59NJL06tXr7Rr1y7bbLNN9t5775x99tl58sknN0o8AQAAAJq2jboDhf/PDhQAGoL/skpj47+q0tj4OUlj5GflB7NF70ABAAAAaEgCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAVNKqAsX748Y8aMyWc/+9nssssuadmyZdq2bZu99947p5xySiZNmlSvecaPH59jjjkmnTp1SsuWLdOpU6ccc8wxGT9+/Eb+BAAAAEBT1LyhF1Bfs2fPzpFHHpmnnnpqre8vX748zz33XJ577rn86le/ytlnn50rrrgiVVVV68xRU1OT008/PaNGjVrr+y+//HJuvfXW3HrrrTn11FNzzTXX1Pp6AAAAYMvUJHagVFdXrxVPPvrRj+a6667Lww8/nLvvvjvnn39+2rRpkyQZMWJELr/88lrn+c53vlOJJ/vtt1/Gjh2byZMnZ+zYsdlvv/2SJKNGjcp3v/vdTfCpAAAAgKaiqqampqahF1Hyxz/+MV/84heTJAceeGAeeOCBbLXVVmuNefTRR3PggQfmnXfeyYc+9KHMmzcvzZv//w02M2bMSI8ePVJdXZ1evXpl4sSJad26deX84sWL079//0yZMiXNmzfP9OnTs+eee26wzzBnzpx07tw5yardNJ06ddpgcwPA+nT59riGXgKsZdYPj2zoJcBa/JykMfKz8oPZWL9/N4kdKA899FDl+H/9r/+1TjxJkv333z9HHXVUkuSNN97I9OnT1zo/YsSIVFdXJ0lGjhy5VjxJkm222SYjR45MsmrHy1VXXbUhPwIAAADQhDWJgLJ8+fLK8R577LHecWvuGFm2bFnluKamJrfffnuSpHv37unbt2+tr+/bt2/23nvvJMltt92WJrA5BwAAANgEmkRA6datW+X4hRdeWO+4mTNnJkmqqqqy1157Vb7/4osv5uWXX06S9O/fv873Wn1+zpw5mTVr1vtdMgAAALAZaRIB5ctf/nK22267JMmll16aFStWrDNm6tSpGTdu1fWLgwYNqoxPkmnTplWOu3fvXud7rXl+zdeVzJkzp84/c+fOrfdcAAAAQOPSJB5j3KFDh1x33XU5/vjj89BDD6V3794ZNmxYunXrloULF+ahhx7KFVdckeXLl+ff/u3fcuWVV671+tmzZ1eOSzePWX2jmXe/rmTN1wEAAACblyYRUJLk6KOPzpQpU3LllVfm2muvzUknnbTW+Z133jkXXXRRTj311MojjVd7++23K8dt27at833WfO3ChQs3wMoBAACApq7JBJR33nknN910U+64445ab+766quvZuzYsenWrVuOPHLtRz4tXbq0ctyiRYs636dly5aV4yVLltR7faXdKnPnzk2fPn3qPR8AAADQeDSJgLJo0aIMGDAgEydOzFZbbZXzzjsvJ598cvbYY48sXbo0//f//t/87//9v/Pggw/mc5/7XEaMGJGzzjqr8vpWrVpVjtd8ok9t1nx6z7sfdVyXDfVcaQAAAKDxaRI3kb3gggsyceLEJMmYMWNy6aWXpnv37mnRokW22267fOYzn8l9992XQw89NDU1NfnmN7+ZJ598svL6bbfdtnJcuixn0aJFlePS5T4AAADAlqHRB5Sampr86le/SrLqccbvvvfJas2bN8/3vve9JMnKlSsrr0nW3h0yZ86cOt9vzUtx3BgWAAAASJpAQHn11Vfz+uuvJ0n222+/Osfuv//+lePp06dXjnv27Fnr92uz5vkePXq8p7UCAAAAm6dGH1CaN///t2mprq6uc+w777xT6+u6du2ajh07JkkmTJhQ5xyrLxXadddd06VLl/e6XAAAAGAz1OgDSvv27bPddtslSR5++OE6I8qacaRr166V46qqqgwcODDJqh0mkyZNqvX1kyZNquxAGThwYKqqqj7w+gEAAICmr9EHlGbNmlUeS/zKK6/kkksuqXXcG2+8kW9961uVr4866qi1zg8bNqyyK2Xo0KHrPKJ4yZIlGTp0aJJVu1eGDRu2oT4CAAAA0MQ1+oCSJOeff3622WabJMmFF16Yz3/+8/njH/+YqVOn5uGHH86IESPyb//2b3nmmWeSJJ/61Kdy2GGHrTVHt27dcu655yZJpkyZkn79+uXmm2/OlClTcvPNN6dfv36ZMmVKkmT48OHZa6+9NuEnBAAAABqz5uUhDa979+65/fbb8+Uvfznz58/PHXfckTvuuKPWsZ/85Cfz+9//vtZzl1xySebNm5drr702U6dOzaBBg9YZM2TIkFx88cUbdP0AAABA09YkdqAkyac//elMnz49l156aQ455JB06NAhW2+9dVq3bp2uXbvmuOOOy2233Za//OUv+dCHPlTrHM2aNcuYMWMybty4DBw4MB07dkyLFi3SsWPHDBw4MHfeeWdGjx6dZs2azF8LAAAAsAk0iR0oq+2www4577zzct55532geQYMGJABAwZsoFUBAAAAmztbLQAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKmlxAmT9/fi677LL069cvH/7wh9OyZct07NgxBxxwQIYPH56HH364OMf48eNzzDHHpFOnTmnZsmU6deqUY445JuPHj98EnwAAAABoapo39ALei9///vc544wz8q9//Wut78+dOzdz587N5MmT8/zzz+e2226r9fU1NTU5/fTTM2rUqLW+//LLL+fWW2/NrbfemlNPPTXXXHNNqqqqNtbHAAAAAJqYJhNQfv3rX+fkk0/OypUrs9NOO+WMM87IQQcdlPbt2+ef//xnZs6cmTvuuCNbb731euf4zne+U4kn++23X84777zsueeemTlzZi677LJMnTo1o0aNSocOHXLxxRdvqo8GAAAANHJNIqBMmzYtp556alauXJmDDz44d9xxR7bffvt1xg0dOjTLly+vdY4ZM2bksssuS5L06tUrEydOTOvWrZMkvXv3zuc///n0798/U6ZMyaWXXpqTTz45e+6558b7UAAAAECT0STugTJ06NAsW7YsO+64Y2655ZZa48lqLVq0qPX7I0aMSHV1dZJk5MiRlXiy2jbbbJORI0cmSaqrq3PVVVdtmMUDAAAATV6jDyjTp0/PvffemyT5+te/nh133PE9z1FTU5Pbb789SdK9e/f07du31nF9+/bN3nvvnSS57bbbUlNT8z5XDQAAAGxOGn1A+f3vf185PvbYYyvHb7zxRp5//vl1bihbmxdffDEvv/xykqR///51jl19fs6cOZk1a9b7WDEAAACwuWn090CZNGlSkmT77bdPjx49cuONN+ayyy7Lk08+WRnTtWvXnHTSSTnnnHPStm3bdeaYNm1a5bh79+51vt+a56dNm5auXbvWa51z5syp8/zcuXPrNQ8AAADQ+DT6gPLMM88kSbp06ZKhQ4fmpz/96TpjXnzxxVx44YX5wx/+kD//+c/p2LHjWudnz55dOe7UqVOd79e5c+daX1ey5usAAACAzUujv4Tn9ddfT7LqXig//elP065du1xzzTWZN29eli5dmkceeSRHHHFEkuTpp5/Osccem5UrV641x9tvv105rm2HypratGlTOV64cOGG+hgAAABAE9bod6AsWrQoSbJs2bJstdVWueuuu9a6CWyvXr3ypz/9KUcddVTuuuuu/O1vf8stt9ySL37xi5UxS5curRyv7yk9q7Vs2bJyvGTJknqvs7RbZe7cuenTp0+95wMAAAAaj0YfUFq1alWJKMcee2ytT9Bp1qxZfvSjH+Wuu+5KkowdO3atgNKqVavK8fLly+t8v2XLllWO3/2o47qULg0CAAAAmq5GfwnPtttuWzlefalObfbZZ5/suuuuSZJHHnlkvXOULstZHWuS8uU+AAAAwJah0QeUNW/OWt8bwM6bN2+t76/5utLTcta8FMeNYQEAAICkCQSUffbZp3K8YsWKOseuPt+8+dpXJvXs2bNyPH369DrnWPN8jx496r1OAAAAYPPV6APKJz7xicrxzJkz6xz7wgsvJEnlUp7VunbtWnm08YQJE+qcY+LEiZU5unTp8l6XCwAAAGyGGn1A+fznP5+tt946SXLLLbesd9yECRPyr3/9K0ly8MEHr3WuqqoqAwcOTLJqh8mkSZNqnWPSpEmVHSgDBw5MVVXVB14/AAAA0PQ1+oCyww475Ktf/WqS5J577slvf/vbdca8/fbbGTZsWOXr0047bZ0xw4YNq1zaM3To0HUeUbxkyZIMHTo0yapLgNacDwAAANiyNfqAkiQXXXRRdttttyTJV77ylQwdOjT33XdfHn300Vx33XXp06dPHn/88STJGWeckd69e68zR7du3XLuuecmSaZMmZJ+/frl5ptvzpQpU3LzzTenX79+mTJlSpJk+PDh2WuvvTbNhwMAAAAaveblIQ2vQ4cOGT9+fD7/+c9nxowZ+clPfpKf/OQn64w75ZRTcvXVV693nksuuSTz5s3Ltddem6lTp2bQoEHrjBkyZEguvvjiDbp+AAAAoGlrEjtQklVPxHn88cfzox/9KAcccEDat2+fFi1apFOnTvnSl76Uv/71rxkzZkzlfim1adasWcaMGZNx48Zl4MCB6dixY1q0aJGOHTtm4MCBufPOOzN69Og0a9Zk/loAAACATaBJ7EBZrU2bNjn33HMrl+K8XwMGDMiAAQM20KoAAACAzZ2tFgAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAQZMOKOedd16qqqoqf+6///7ia8aPH59jjjkmnTp1SsuWLdOpU6ccc8wxGT9+/MZfMAAAANAkNdmA8sQTT2TEiBH1Hl9TU5PTTjstRxxxRG699da8/PLLWb58eV5++eXceuutOeKII3LaaaelpqZmI64aAAAAaIqaZEBZuXJlvva1r6W6ujo77bRTvV7zne98J6NGjUqS7Lfffhk7dmwmT56csWPHZr/99kuSjBo1Kt/97nc32roBAACApqlJBpQf//jHeeSRR9K9e/cMGTKkOH7GjBm57LLLkiS9evXKQw89lEGDBqV3794ZNGhQHnzwwfTq1StJcumll2bmzJkbdf0AAABA09LkAsrs2bMru0R+/vOfp0WLFsXXjBgxItXV1UmSkSNHpnXr1mud32abbTJy5MgkSXV1da666qoNu2gAAACgSWtyAeXMM8/MwoULc9JJJ+WQQw4pjq+pqcntt9+eJOnevXv69u1b67i+fftm7733TpLcdttt7oUCAAAAVDSpgPK73/0uf/rTn9K+ffv86Ec/qtdrXnzxxbz88stJkv79+9c5dvX5OXPmZNasWR9orQAAAMDmo3lDL6C+FixYkLPOOivJqvuUdOjQoV6vmzZtWuW4e/fudY5d8/y0adPStWvXeq9vzpw5dZ6fO3duvecCAAAAGpcmE1DOO++8/POf/8z//J//s143jl1t9uzZleNOnTrVObZz5861vq4+1nwtAAAAsHlpEpfwPPjggxk9enSaN2+ea665JlVVVfV+7dtvv105btu2bZ1j27RpUzleuHDhe18oAAAAsFlq9DtQli9fnlNPPTU1NTU5++yzs++++76n1y9durRyXHpiT8uWLSvHS5YseU/vU9qxMnfu3PTp0+c9zQkAAAA0Do0+oHz/+9/PtGnTsttuu+WCCy54z69v1apV5Xj58uV1jl22bFnl+N2POi4pXR4EAAAANF2N+hKe6dOn5wc/+EGSZOTIkWtdYlNf2267beW4dFnOokWLKsely30AAACALUej3oEyYsSILF++PHvssUcWL16c3/72t+uMefrppyvHf/3rX/PPf/4zSfK5z30ubdq0WWtnSOlJOWtehuOmsAAAAMBqjTqgrL6k5oUXXsiXv/zl4vjvfe97leMXX3wxbdq0Sc+ePSvfmz59ep2vX/N8jx493utyAQAAgM1Uo76EZ0Po2rVrOnbsmCSZMGFCnWMnTpyYJNl1113TpUuXjb00AAAAoIlo1AHluuuuS01NTZ1/1ryx7H333Vf5/uoAUlVVlYEDByZZtcNk0qRJtb7XpEmTKjtQBg4c+J4elQwAAABs3hp1QNlQhg0blubNV12tNHTo0HUeUbxkyZIMHTo0SdK8efMMGzZsUy8RAAAAaMS2iIDSrVu3nHvuuUmSKVOmpF+/frn55pszZcqU3HzzzenXr1+mTJmSJBk+fHj22muvhlwuAAAA0Mg06pvIbkiXXHJJ5s2bl2uvvTZTp07NoEGD1hkzZMiQXHzxxQ2wOgAAAKAx2yJ2oCRJs2bNMmbMmIwbNy4DBw5Mx44d06JFi3Ts2DEDBw7MnXfemdGjR6dZsy3mrwQAAACopya/A+XCCy/MhRdeWO/xAwYMyIABAzbeggAAAIDNju0WAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAVNIqA89thj+f73v58jjjginTt3TsuWLdO2bdt069YtgwcPzgMPPPCe5hs/fnyOOeaYdOrUKS1btkynTp1yzDHHZPz48RvpEwAAAABNWfOGXkBJ//79M3HixHW+v3z58jz//PN5/vnnc/311+crX/lKRo8enRYtWqx3rpqampx++ukZNWrUWt9/+eWXc+utt+bWW2/NqaeemmuuuSZVVVUb/LMAAAAATVOj34Hy8ssvJ0k6duyYs846K3/4wx8yefLkPPzww7nyyiuz6667JkluuOGGDB48uM65vvOd71TiyX777ZexY8dm8uTJGTt2bPbbb78kyahRo/Ld7353430gAAAAoMmpqqmpqWnoRdTlqKOOyoknnpgvfOEL2WqrrdY5P3/+/PTr1y/PPfdckmTixIk5+OCD1xk3Y8aM9OjRI9XV1enVq1cmTpyY1q1bV84vXrw4/fv3z5QpU9K8efNMnz49e+655wb7HHPmzEnnzp2TJLNnz06nTp022NwAsD5dvj2uoZcAa5n1wyMbegmwFj8naYz8rPxgNtbv341+B8qf/vSnHHfccbXGkyTZcccdc8UVV1S+/sMf/lDruBEjRqS6ujpJMnLkyLXiSZJss802GTlyZJKkuro6V1111QZYPQAAALA5aPQBpT4OOeSQyvHMmTPXOV9TU5Pbb789SdK9e/f07du31nn69u2bvffeO0ly2223pZFvzgEAAAA2kc0ioCxfvrxy3KzZuh/pxRdfrNxLpX///nXOtfr8nDlzMmvWrA23SAAAAKDJavRP4amPCRMmVI67d+++zvlp06bVeX5Na56fNm1aunbtWq81zJkzp87zc+fOrdc8AAAAQOPT5APKypUr88Mf/rDy9XHHHbfOmNmzZ1eOSzePWX2jmXe/rmTN1wEAAACblyZ/Cc+IESMyefLkJMnRRx+dXr16rTPm7bffrhy3bdu2zvnatGlTOV64cOEGWiUAAADQlDXpHSgTJkzIt7/97STJTjvtlJ///Oe1jlu6dGnluEWLFnXO2bJly8rxkiVL6r2W0m6VuXPnpk+fPvWeDwAAAGg8mmxA+fvf/56jjz461dXVadmyZX73u99l5513rnVsq1atKsdr3nC2NsuWLascv/tRx3XZUM+VBgAAABqfJnkJz4svvpjDDjssb7zxRrbaaquMHTu2zqfrbLvttpXj0mU5ixYtqhyXLvcBAAAAtgxNLqC88sor+fSnP51XXnklVVVVufbaa3P00UfX+Zo1d4eUnpaz5qU4bgwLAAAAJE0soMyfPz+f+cxn8sILLyRJRo4cmRNPPLH4up49e1aOp0+fXufYNc/36NHjfa4UAAAA2Jw0mYDy5ptv5vDDD88zzzyTJPnhD3+Y//zP/6zXa7t27ZqOHTsmWXXj2bpMnDgxSbLrrrumS5cu73/BAAAAwGajSQSUxYsX58gjj8xjjz2WJPnv//7vfOtb36r366uqqjJw4MAkq3aYTJo0qdZxkyZNquxAGThwYKqqqj7gygEAAIDNQaMPKMuXL8/RRx+dhx56KEly1lln5eKLL37P8wwbNizNm6966NDQoUPXeUTxkiVLMnTo0CRJ8+bNM2zYsA+2cAAAAGCz0egfY/zlL385d999d5Lkk5/8ZIYMGZKnn356veNbtGiRbt26rfP9bt265dxzz80Pf/jDTJkyJf369cu3vvWt7Lnnnpk5c2YuvfTSTJ06NUkyfPjw7LXXXhvnAwEAAABNTqMPKLfcckvl+K9//Ws++tGP1jl+9913z6xZs2o9d8kll2TevHm59tprM3Xq1AwaNGidMUOGDHlfO1wAAACAzVejv4RnQ2rWrFnGjBmTcePGZeDAgenYsWNatGiRjh07ZuDAgbnzzjszevToNGu2Rf21AAAAAAWNfgdKTU3NBp9zwIABGTBgwAafFwAAANg82WoBAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFzRt6AfB+dfn2uIZeAqxl1g+PbOglAAAAG4kdKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFAgoAAABAgYACAAAAUCCgAAAAABQIKAAAAAAFW2RAeemll3LuueemR48eadOmTdq3b58+ffrk8ssvz+LFixt6eQAAAEAj07yhF7CpjRs3Lscff3zefPPNyvcWL16cRx55JI888khGjx6dO++8M3vssUcDrhIAAABoTLaoHShPPPFEjjvuuLz55ptp27ZtLrnkkvztb3/Lvffem6997WtJkmeffTZHHnlkFi5c2MCrBQAAABqLLWoHyrBhw7J48eI0b948d999dw488MDKuU9+8pPZa6+9ct5552X69Om58sorc/755zfgagEAAIDGYovZgfLII4/k/vvvT5IMGTJkrXiy2jnnnJMePXokSa666qq88847m3KJAAAAQCO1xQSU2267rXJ88skn1zqmWbNmOfHEE5Mkb7zxRiW4AAAAAFu2LSagPPDAA0mSNm3aZP/991/vuP79+1eOH3zwwY2+LgAAAKDx22LugTJt2rQkyUc+8pE0b77+j929e/d1XlMfc+bMqfP87NmzK8dz586t97ysX/Vb8xt6CbCW0s8BaAh+VtLY+FlJY+PnJI2Rn5UfzJq/c1dXV2+webeIgLJ06dLMn7/qB2OnTp3qHPuhD30obdq0yaJFi9aKHiWdO3eu99g+ffrUeyzQdHT+eUOvAKDx87MSoMzPyg3ntddeS5cuXTbIXFvEJTxvv/125bht27bF8W3atEkSjzIGAAAAkmxBO1BWa9GiRXF8y5YtkyRLliyp93uUdqssXbo006dPz84775wOHTrUeRkRbCpz586t7IiaPHlydtlllwZeEUDj4uckQJmflTQ21dXVee2115Ik++677wabd4v4Lb5Vq1aV4+XLlxfHL1u2LEnSunXrer9H6dKgZNX9V6Cx2mWXXer1v2OALZWfkwBlflbSWGyoy3bWtEVcwrPttttWjutzWc6iRYuS1O9yHwAAAGDzt0UElFatWmXHHXdMUr6b8RtvvFEJKO/lxrAAAADA5muLCChJ0qNHjyTJjBkz6nyM0fTp09d5DQAAALBl22ICykEHHZRk1eU5jz766HrHTZgwoXLcr1+/jb4uAAAAoPHbYgLKv//7v1eOf/WrX9U6ZuXKlfn1r3+dJGnXrl0OPfTQTbE0AAAAoJHbYgJKnz59cvDBBydJxowZk4cffnidMVdccUWmTZuWJDnrrLOy9dZbb9I1AgAAAI3TFvEY49Wuvvrq9OvXL0uWLMlhhx2W//qv/8qhhx6aJUuW5Le//W1GjRqVJOnWrVvOOeecBl4tAAAA0FhU1dTU1DT0IjalO+64IyeccELeeuutWs9369Yt48aNy0c+8pFNvDIAAACgsdriAkqS/OMf/8jVV1+dcePGZc6cOWnRokU+8pGP5Nhjj83Xv/71bLPNNg29RAAAAKAR2SIDCgAAAMB7scXcRBYAAADg/RJQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQYAv14IMPpqqqqvJn4sSJDb0kgAZ3//33r/Wz8d1/2rZtm27duuWkk07K/fff39DLBWhw77zzTn7729/mpJNOSo8ePbLDDjtk6623zo477pj9998/Z5xxRv7yl79k5cqVDb1U+MCqampqahp6EcCmd+qpp+aXv/xl5eshQ4Zk9OjRDbgigIZ3//3359BDD633+FNOOSWjRo3KVltttRFXBdA43X777fnmN7+ZF154oTi2W7duufLKK3PkkUdugpXBxiGgwBZo2bJl+fCHP5wFCxakbdu2WbhwYbbbbrv885//TOvWrRt6eQANZs2AcsYZZ+TMM8+snKupqcnrr7+ehx9+OCNGjMi8efOSJOeff34uuuiiBlkvQEP5wQ9+kP/+7//O6l8nP/3pT2fgwIHp2bNn2rVrl9dffz3PPvts7rjjjtxzzz1ZuXJlPvaxj+Xxxx9v2IXDByCgwBbod7/7Xb70pS8lScaMGZMhQ4YkScaOHZtBgwY15NIAGtSaAeWCCy7IhRdeWOu4Z555Jr169cqSJUuy3XbbZf78+dl666034UoBGs4NN9yQE088MUnSoUOH3HzzzXXu3nvqqacybNiw/Otf/xJQaNLcAwW2QNdff32SpGfPnjnllFPSs2fPJMmvf/3rhlwWQJPRs2fPyjb0t956K9OmTWvgFQFsGq+88krOOOOMJMk222xTr0sf991339xzzz0599xzN8USYaMRUGALM2/evNx9991JkhNOOCFJcvzxxydJ7r777rz66qsNtjaApqRLly6V46VLlzbcQgA2oREjRmTRokVJkosuuqjyH+JKmjVrVvm3JzRVAgpsYW688cZUV1enqqqqEk6OP/74VFVVZcWKFbnxxhsbeIUATcOsWbMqx7vttlvDLQRgE6mpqansZG7Tpk1OPfXUBl4RbFoCCmxhVv+f3sEHH1z5B//uu++egw46KInLeADqY/r06Rk3blySpHfv3vnwhz/cwCsC2PieeeaZvPbaa0lW/Vtyu+22a+AVwabVvKEXAGw6Tz31VJ544okkWWcL5QknnJAHHnggTzzxRJ566qnsu+++DbFEgEZj3rx5efrppytf19TUZMGCBZWn8Ky+gexVV13VcIsE2IRW/zsyST7+8Y834EqgYQgosAVZvfukZcuWOfbYY9c6d9xxx+Ub3/hGli1bluuvvz6XX355QywRoNH4+c9/np///Oe1nmvWrFlOO+20DBs2LN27d9/EKwNoGPPnz68c77zzzg24EmgYLuGBLcSKFSty0003JUmOPPLItGvXbq3z7dq1y4ABA5IkN910U1asWLGplwjQZKxcuTK/+93vMnr06CxfvryhlwOwSbz99tuV4zZt2jTgSqBhCCiwhbj77rszd+7cJOtevrPa6u/PnTs3f/nLXzbZ2gAaowsuuCA1NTVr/Vm8eHGefPLJDB8+PG+//XauuOKKHHbYYVmyZElDLxdgo9t2220rx6ufxANbEgEFthCrbw7brl27HHnkkbWOWXNnipvJAqyrdevW2XfffXPZZZflZz/7WZJkwoQJ+cEPftDAKwPY+HbcccfK8auvvtqAK4GGIaDAFuCtt97K7bffniRZsGBBWrZsmaqqqnX+tGrVKgsWLEiS3HbbbWtt0wRgbUOGDEn79u2TJGPGjGng1QBsfB/72Mcqx4899lgDrgQahoACW4Df/e5373l7+eLFi/OHP/xhI60IoOlr1qxZ9tprryTJK6+8ktdff72BVwSwcfXs2bOyC+WBBx7IW2+91cArgk3LU3hgC7D6cpxddtklV155ZXH8t771rbz00kv59a9/nZNPPnljLw+gyaqurq4cv/POOw24EoCNr6qqKoMHD87ll1+eRYsWZfTo0fnmN7/Z0MuCTUZAgc3ciy++mAcffDBJ8oUvfCGDBg0qvmbKlCm54oorMmHChLz00kvZbbfdNvYyAZqcxYsX55lnnkmStGrVaq17AwBsroYNG5af/exnWbx4cc4///wMGDCgXo9zX7lyZW666ab1PswAmgKX8MBm7oYbbkhNTU2S5Itf/GK9XrN6XE1NTW644YaNtjaApuyCCy6oXB55+OGHZ6uttmrgFQFsfLvuumt+8pOfJFn1JJ7+/ftnwoQJdb7mmWeeyeGHH57LL798UywRNpqqmtW/WQGbpb322iszZszITjvtlLlz56ZZs3I3rampyW677ZY5c+Zk7733zvTp0zfBSgEa3v33359DDz00SXLGGWfkzDPPXOv80qVL8/zzz+fXv/51xo8fn2TV7pPJkydn33333eTrBWgo3/ve93L++edXvj7ssMMycODA9OjRI+3atcvrr7+e5557LuPGjcv48eOzYsWKfOxjH8vjjz/ecIuGD0hAgc3YQw89lIMOOihJctppp+Waa66p92vPOuus/PjHP06STJo0KQcccMBGWSNAY7JmQKmPDh065De/+U0OO+ywjbgqgMbplltuyTnnnJNZs2YVx+6zzz658sor/bykSXMJD2zGVt88Nll1/5P3Ys3xa84DsCVr0aJFPvzhD+dTn/pUrrjiijz77LN+GQC2WMccc0yeffbZ3HjjjTnhhBOy995750Mf+lCaN2+e9u3b5+Mf/3jOPPPM3HvvvXnqqaf8vKTJswMFAAAAoMAOFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFACATeD+++9PVVVVqqqqcv/99zf0cgCA90hAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUACARmf+/PkZPnx4unXrltatW2fnnXfOZz7zmdx6661Jkuuuu67yRJtZs2at9douXbqkqqoqgwcPTpI8+uijGTx4cLp27ZqWLVumqqpqrfEvvPBCrrjiinzuc59Lly5d0rp167Ru3Tq77757vvSlL2X8+PH1WvOSJUtyySWX5GMf+1jatGmTHXbYIf369csvf/nLrFy5st6fvaamJn/4wx/yhS98IZ07d06rVq3yoQ99KH369Mn3vve9LFiwoN5zAQAbTlVNTU1NQy8CAGC1J554Ip/5zGfy2muv1Xr+1FNPzYEHHpiTTz45SfLiiy+mS5culfNdunTJP/7xj5x00knp27dvhg4dmurq6rXmWP3PnxdffDF77LFHcU0nnHBCfvWrX6V58+a1nn/llVfyqU99KtOnT6/1/Gc/+9mcffbZOfzww5Mk9913Xw455JB1xr322ms5+uij89BDD613LTvvvHNuv/32HHDAAcV1AwAbTu3/CgAAaABvvPFGPvvZz1biyfHHH58TTjghHTp0yIwZM3L11Vdn1KhReeKJJ4pzPfLII/nNb36Tzp0759xzz83++++fFStW5IEHHqiMWbFiRVq0aJHDDz88n/nMZ9KzZ8+0b98+r7/+ep577rn89Kc/zd///vf85je/yR577JGLLrponfeprq7OUUcdVYknhx12WM4444x07tw5L730Un72s59l/Pjx+de//lXnehctWpT+/ftn2rRpadGiRU4++eQMGDAgnTt3zqJFizJx4sRceeWVefXVV3PEEUdk6tSp2X333d/LXy8A8AHYgQIANBpnnXVWfvzjHydJLr/88pxzzjlrnV+xYkW+8IUv5Pbbb698b307UJJk3333zcSJE9OuXbta32/RokV56623sssuu9R6vqamJqecckquu+66tGnTJi+//HK23377tcaMHDky3/jGN5Ks2h3zi1/8Yp15hgwZkmuvvbbydW07UIYOHZqf/OQn2X777fOXv/wlvXr1Wmeef/zjHznwwAMzd+7cnHDCCbnhhhtqXTcAsOEJKABAo7B06dJ8+MMfzptvvpmPf/zjmTJlyjr3K0mSV199NV26dMnSpUuT1B1QJk6cmIMPPvgDrev111/PTjvtlBUrVlTuTbKmnj17Ztq0adl5553zwgsvZJtttllnjoULF2aPPfao7Kx5d0CZP39+OnfunKVLl+bqq6+uBJna/PznP8+ZZ56ZrbfeOgsWLKj1/QCADc9NZAGARuHRRx/Nm2++mSQ58cQTa40nyap7gKy+l0hdOnfu/J7jyTvvvJM5c+Zk2rRpefrpp/P000/nlVdeyQ477JAk61w69Morr2TatGlJkuOOO269MaNt27Y57rjj1vu+f/7znytBqK5xSfKJT3yistZHH320fh8MAPjA3AMFAGgUnn766crx/vvvX+fYXr16rXUZT20++tGP1ut933nnnYwaNSo33HBDpk6dmuXLl6937Pz589f6+qmnnqoc9+7du8736dOnT37605/Wem7KlCmV4/VdTlSbf/7zn/UeCwB8MAIKANAovPHGG5XjnXbaqc6xHTp0KM73oQ99qDjm9ddfz2GHHVbvnRxLlixZ6+v3suadd955vefmzZtXr/d/t8WLF7+v1wEA752AAgBslrbaaqvimLPOOqsST/793/89p5xySj760Y9mp512SqtWrSqXEe22226ZPXt23n3ruDW/Xt8lR7WNfbcVK1YkSVq0aPGeLsvp1KlTvccCAB+MgAIANApr7hiZN29eunXrtt6xq2/G+kG89dZbufnmm5Mk//Ef/5Ebb7xxvWPX3Gmypvbt21eOX3311Trfr65dJqvvsbJ8+fLssMMO7+kyHgBg03ATWQCgUdhnn30qx2veE6Q2pfP18fzzz+edd95JkgwaNGi945599tksXLiw1nP77rtv5fiRRx6p8/3qOr/ffvtVju++++465wEAGoaAAgA0Cr169cr222+fJLnhhhvWe8nLq6++mj//+c8f+P2qq6srx3XdS+Saa65Z77mOHTumR48eSZLf//7369wjZbVFixbld7/73XrnOeKII7L11lsnSUaMGLHW2gCAxkFAAQAahVatWuXEE09Mkjz22GO58sor1xmzcuXKnHbaaZVH/n4QH/nIRyr3Lfn1r39d65g//elPGTlyZJ3znHHGGUlWPRHnnHPOqXXM2WefXeclPLvuumtOPvnkJKselXzaaafVGVHmzZuX0aNH17kuAGDDqqqp645mAACb0Ouvv5599tmn8nje448/Pl/5ylfSoUOHzJgxI1dffXX+9re/pU+fPpk8eXKSZNasWdl9990rc3Tp0iX/+Mc/ctJJJ+W6666r8/2OOuqojBs3Lkly+OGH57TTTstuu+2WefPm5Y9//GOuu+667LHHHlmwYEFee+21Wuesrq5Onz59MnXq1CTJZz/72Zx++unp3LlzZs+enZ/97Ge5++6707t378plPPfdd18OOeSQteZZuHBhDjzwwMrjnHv27JlTTz01+++/f9q2bZsFCxbk73//e/7yl7/kzjvvzL777rtBLmUCAOpHQAEAGpUnnngin/nMZ9Z7o9jBgwfn4IMPzpAhQ5Ks2vmx5iOC30tAmT17dg466KC89NJLtZ7fbbfdctddd2XAgAF1zvnKK6/kk5/8ZJ599tla5znssMNyzjnn5PDDD09Se0BJVgWk448/PuPHj69z3Uly6KGH5q9//WtxHACwYbiEBwBoVD72sY/lmWeeyTnnnJO99torLVu2zI477phDDz00N910U371q1/lrbfeqoxffd+U96Nz58557LHHMnz48HTr1i0tW7bM9ttvn4997GO54IIL8vjjj6dnz57FeTp27JipU6fm4osvzv/4H/8jrVu3Trt27dK3b9/87Gc/y1133ZUWLVoU52nfvn3uuuuu3HvvvTn55JOz1157pW3btmnevHnat2+f3r175z//8z9z55135p577nnfnxsAeO/sQAEAmpyvfvWrGTNmTDp16pTZs2c39HIAgC2AHSgAQJOyZMmS3H777UmSvn37NvBqAIAthYACADQqM2fOXO8jjFesWJEzzjgj8+fPT5KcdNJJm3JpAMAWzCU8AECjMnjw4EyePDmDBg3KAQcckJ122ilLlizJk08+mV/+8pd57LHHkiSf+tSncs8991QeRQwAsDE1b+gFAAC827Rp03LBBRes93y/fv1y8803iycAwCZjBwoA0Kg8++yz+eMf/5h77rkn//jHP/Laa6/lnXfeyQ477JBevXrlS1/6UgYNGpRmzVyJDABsOgIKAAAAQIH/dAMAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFPw/guEmO+8ax8cAAAAASUVORK5CYII="/>


```python
# 메서드 체이닝
```


```python
# A, B, C, D 등급 변수 만들기

mpg['grade2'] = np.where(mpg['total'] >= 30, 'A',
                np.where(mpg['total'] >= 25, 'B',
                np.where(mpg['total'] >= 20, 'C', 'D')))
mpg
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>category</th>
      <th>total</th>
      <th>test</th>
      <th>grade</th>
      <th>grade2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>18</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
      <td>23.5</td>
      <td>pass</td>
      <td>B</td>
      <td>C</td>
    </tr>
    <tr>
      <th>1</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
      <td>25.0</td>
      <td>pass</td>
      <td>B</td>
      <td>B</td>
    </tr>
    <tr>
      <th>2</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>20</td>
      <td>31</td>
      <td>p</td>
      <td>compact</td>
      <td>25.5</td>
      <td>pass</td>
      <td>B</td>
      <td>B</td>
    </tr>
    <tr>
      <th>3</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(av)</td>
      <td>f</td>
      <td>21</td>
      <td>30</td>
      <td>p</td>
      <td>compact</td>
      <td>25.5</td>
      <td>pass</td>
      <td>B</td>
      <td>B</td>
    </tr>
    <tr>
      <th>4</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>compact</td>
      <td>21.0</td>
      <td>pass</td>
      <td>B</td>
      <td>C</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>229</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>19</td>
      <td>28</td>
      <td>p</td>
      <td>midsize</td>
      <td>23.5</td>
      <td>pass</td>
      <td>B</td>
      <td>C</td>
    </tr>
    <tr>
      <th>230</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>midsize</td>
      <td>25.0</td>
      <td>pass</td>
      <td>B</td>
      <td>B</td>
    </tr>
    <tr>
      <th>231</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
      <td>21.0</td>
      <td>pass</td>
      <td>B</td>
      <td>C</td>
    </tr>
    <tr>
      <th>232</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>18</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
      <td>22.0</td>
      <td>pass</td>
      <td>B</td>
      <td>C</td>
    </tr>
    <tr>
      <th>233</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>3.6</td>
      <td>2008</td>
      <td>6</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>17</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
      <td>21.5</td>
      <td>pass</td>
      <td>B</td>
      <td>C</td>
    </tr>
  </tbody>
</table>
<p>234 rows × 15 columns</p>
</div>



```python
count_grade_2 = mpg['grade2'].value_counts().sort_index()
count_grade_2
```

<pre>
grade2
A     10
B     33
C     85
D    106
Name: count, dtype: int64
</pre>

```python
count_grade_2.plot.bar(rot=0)
```

<pre>
<Axes: xlabel='grade2'>
</pre>
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABFAAAANhCAYAAADABk+6AAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjcuMiwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8pXeV/AAAACXBIWXMAAB7CAAAewgFu0HU+AABK4UlEQVR4nO3de5TXZaHv8c/gOIDgDUUTQcELAh5ruwXEjYaWl0STrabR1lJjp1mbxLzUOZXmTktNRSPNTWBeKtLMy1KUvKTijaMoeUlQQVFAEk1N5T4y5w8XvwMyzDMoMDPweq3FWs/M9/k9v+fHckTefi9VdXV1dQEAAABgpVo19QYAAAAAmjsBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACqqbegPriwULFuSZZ55JknTs2DHV1X7rAQAAYHWrra3NG2+8kSTZbbfd0qZNm9Wyrr/FryXPPPNM+vbt29TbAAAAgPXGY489lj59+qyWtVzCAwAAAFDgDJS1pGPHjpXxY489lm222aYJdwMAAADrptmzZ1euAFn27+KflICylix7z5NtttkmnTt3bsLdAAAAwLpvdd5/1CU8AAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFFQ39QYAAABYu7p+f2xTb4G1aPr5hzT1FtYJzkABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAArWaECZM2dObr/99px11lk5+OCDs+WWW6aqqipVVVU5/vjjV3m9cePG5Ygjjkjnzp3TunXrdO7cOUcccUTGjRvX6DXmzZuXn//85+nbt286dOiQ9u3bp2fPnjn99NPz6quvrvKeAAAAgHVf9ZpcfOutt14t69TV1eWb3/xmRo4cudz3Z82alZtvvjk333xzTjzxxFx55ZWpqqpa6TrTpk3LIYcckueff36570+ZMiVTpkzJqFGj8vvf/z4DBw5cLfsGAAAA1g1r7RKeLl265MADD/xYr/3hD39YiSe77757xowZk8ceeyxjxozJ7rvvniQZOXJkfvSjH610jffffz+HHnpoJZ584xvfyL333ptHHnkk5513Xtq3b59//vOfOeqoo/L0009/rH0CAAAA66Y1egbKWWedlT59+qRPnz7ZeuutM3369HTr1m2V1pg6dWouvPDCJEnv3r0zfvz4tG3bNknSp0+fHHbYYRkwYEAmTpyYCy64ICeccEJ23HHHFda56KKLMmXKlCTJhRdemDPOOKNybK+99sp+++2Xz372s5k3b16GDRuWv/zlLx/3YwMAAADrmDV6Bso555yTQw899BNdyjN8+PDU1tYmSUaMGFGJJ0tttNFGGTFiRJKktrY2l1566QprLF68OJdddlmSpGfPnjnttNNWmLPXXntlyJAhSZL77rsvTzzxxMfeMwAAALBuadZP4amrq8utt96aJOnRo0f69etX77x+/fpll112SZLccsstqaurW+74/fffn3feeSdJctxxx6VVq/o/9rI3tr3ppps+4e4BAACAdUWzDigvv/xyZs2alSQZMGBAg3OXHp85c2amT5++3LEHH3xwhXn16d27d9q1a5ckeeihhz7OlgEAAIB10Bq9B8onNXny5Mq4R48eDc5d9vjkyZOXu9dKY9eprq7OjjvumKeffnq51zTGzJkzGzw+e/bsVVoPAAAAaD6adUCZMWNGZdy5c+cG53bp0qXe1y37dbt27bLZZpsV13n66afzxhtvZOHChWndunWj9rrs+wMAAADrlmZ9Cc97771XGbdv377BuUsvvUk+fGRxfeuU1iitAwAAAKyfmvUZKAsWLKiMa2pqGpy77Jki8+fPr3ed0hqldRry0bNePmr27Nnp27dvo9cDAAAAmo9mHVDatGlTGS9atKjBuQsXLqyMP/qo46XrlNYordOQ0iVGAAAAQMvVrC/h2XjjjSvj0uU0c+fOrYw/eqnO0nUac0lOQ+sAAAAA66dmHVCWPauj9JSbZS+h+egNXZeuM3fu3LzzzjuNWqdjx46NvoEsAAAAsG5r1gGlV69elfGUKVManLvs8Z49e36sdWprazNt2rR61wAAAADWX806oHTr1i2dOnVKkjzwwAMNzh0/fnySZNttt03Xrl2XO7b33ntXxg2tM3HixMolPP379/84WwYAAADWQc06oFRVVWXQoEFJPjxzZMKECfXOmzBhQuXMkkGDBqWqqmq54/vuu2823XTTJMk111yTurq6ete5+uqrK+PDDz/8k24fAAAAWEc064CSJMOGDUt19YcPCxo6dOgKjxaeP39+hg4dmiSprq7OsGHDVlijpqYm3/nOd5IkkydPzkUXXbTCnEcffTSjR49OkgwYMCB9+vRZnR8DAAAAaMHW6GOMH3rooUydOrXy9ZtvvlkZT506dbkzPpLk+OOPX2GN7t275/TTT8/555+fiRMnpn///vne976XHXfcMdOmTcsFF1yQSZMmJUnOOOOM7LzzzvXu5Ywzzsj111+fF154IWeeeWamTp2awYMHp23btrnvvvvy05/+NLW1tWnbtm0uvfTST/zZAQAAgHVHVd3KrmdZDY4//vhcc801jZ6/sq0sWbIk3/jGN3LVVVet9LVDhgzJyJEj06rVyk+qmTp1agYOHJgXX3yx3uObbLJJfve73+XQQw9t9J4ba+bMmZWnA82YMWO5JwwBAACsTV2/P7apt8BaNP38Q5p6C2vVmvr7d7O/hCdJWrVqldGjR2fs2LEZNGhQOnXqlJqamnTq1CmDBg3KHXfckVGjRjUYT5Jkp512yqRJk3LBBRekd+/e2WyzzbLRRhtll112yamnnpqnn356jcQTAAAAoGVbo2eg8P85AwUAAGgunIGyfnEGynp0BgoAAABAUxJQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAICC6qbeAAAAzVPX749t6i2wFk0//5Cm3gJAs+YMFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKGhRAWXRokUZPXp0vvCFL2SbbbZJ69at0759++yyyy75+te/ngkTJjRqnXHjxuWII45I586d07p163Tu3DlHHHFExo0bt4Y/AQAAANASVTf1BhprxowZOeSQQ/LMM88s9/1FixblhRdeyAsvvJDf/OY3OfXUU3PxxRenqqpqhTXq6uryzW9+MyNHjlzu+7NmzcrNN9+cm2++OSeeeGKuvPLKel8PAAAArJ9axBkotbW1y8WTT3/607n66qvz6KOP5q677spZZ52Vdu3aJUmGDx+eiy66qN51fvjDH1biye67754xY8bksccey5gxY7L77rsnSUaOHJkf/ehHa+FTAQAAAC1FVV1dXV1Tb6LkT3/6U770pS8lSfbaa688+OCD2WCDDZab88QTT2SvvfbK4sWLs/nmm2fOnDmprv7/J9hMnTo1PXv2TG1tbXr37p3x48enbdu2lePz5s3LgAEDMnHixFRXV2fKlCnZcccdV9tnmDlzZrp06ZLkw7NpOnfuvNrWBgBYE7p+f2xTb4G1aPr5hzT1FliL/HyvX9a3n+819ffvFnEGysMPP1wZ/+///b9XiCdJsscee+TQQw9Nkrz99tuZMmXKcseHDx+e2traJMmIESOWiydJstFGG2XEiBFJPjzj5dJLL12dHwEAAABowVpEQFm0aFFlvMMOO6x03rJnjCxcuLAyrqury6233pok6dGjR/r161fv6/v165dddtklSXLLLbekBZycAwAAAKwFLSKgdO/evTJ+6aWXVjpv2rRpSZKqqqrsvPPOle+//PLLmTVrVpJkwIABDb7X0uMzZ87M9OnTP+6WAQAAgHVIiwgoX/nKV7LJJpskSS644IJ88MEHK8yZNGlSxo798Dq+wYMHV+YnyeTJkyvjHj16NPheyx5f9nUlM2fObPDX7NmzG70WAAAA0Ly0iMcYd+zYMVdffXWOOeaYPPzww+nTp0+GDRuW7t275/3338/DDz+ciy++OIsWLcq//Mu/5JJLLlnu9TNmzKiMSzePWXqjmY++rmTZ1wEAAADrlhYRUJLk8MMPz8SJE3PJJZfkqquuynHHHbfc8a233jrnnHNOTjzxxMojjZd67733KuP27ds3+D7Lvvb9999fDTsHAAAAWroWE1AWL16c3//+97ntttvqvbnr66+/njFjxqR79+455JDlH9G0YMGCyrimpqbB92ndunVlPH/+/Ebvr3S2yuzZs9O3b99GrwcAAAA0Hy0ioMydOzcDBw7M+PHjs8EGG+TMM8/MCSeckB122CELFizI//2//zf//d//nYceeihf/OIXM3z48JxyyimV17dp06YyXvaJPvVZ9uk9H33UcUNW13OlAQAAgOanRdxE9uyzz8748eOTJKNHj84FF1yQHj16pKamJptsskkOOOCA3Hfffdlvv/1SV1eX7373u3n66acrr994440r49JlOXPnzq2MS5f7AAAAAOuHZh9Q6urq8pvf/CbJh48z/ui9T5aqrq7OT37ykyTJkiVLKq9Jlj87ZObMmQ2+37KX4rgxLAAAAJC0gIDy+uuv56233kqS7L777g3O3WOPPSrjKVOmVMa9evWq9/v1WfZ4z549V2mvAAAAwLqp2QeU6ur/f5uW2traBucuXry43td169YtnTp1SpI88MADDa6x9FKhbbfdNl27dl3V7QIAAADroGYfUDp06JBNNtkkSfLoo482GFGWjSPdunWrjKuqqjJo0KAkH55hMmHChHpfP2HChMoZKIMGDUpVVdUn3j8AAADQ8jX7gNKqVavKY4lfe+21nHfeefXOe/vtt/O9732v8vWhhx663PFhw4ZVzkoZOnToCo8onj9/foYOHZrkw7NXhg0btro+AgAAANDCNfuAkiRnnXVWNtpooyTJj3/84xx22GH505/+lEmTJuXRRx/N8OHD8y//8i957rnnkiSf//znc+CBBy63Rvfu3XP66acnSSZOnJj+/fvn+uuvz8SJE3P99denf//+mThxYpLkjDPOyM4777wWPyEAAADQnFWXpzS9Hj165NZbb81XvvKVvPnmm7ntttty22231Tv3c5/7XP74xz/We+y8887LnDlzctVVV2XSpEkZPHjwCnOGDBmSc889d7XuHwAAAGjZWsQZKEmy//77Z8qUKbnggguy7777pmPHjtlwww3Ttm3bdOvWLUcffXRuueWW3HPPPdl8883rXaNVq1YZPXp0xo4dm0GDBqVTp06pqalJp06dMmjQoNxxxx0ZNWpUWrVqMb8tAAAAwFrQIs5AWWqLLbbImWeemTPPPPMTrTNw4MAMHDhwNe0KAAAAWNc51QIAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAApaXEB58803c+GFF6Z///751Kc+ldatW6dTp07Zc889c8YZZ+TRRx8trjFu3LgcccQR6dy5c1q3bp3OnTvniCOOyLhx49bCJwAAAABamuqm3sCq+OMf/5iTTz45//jHP5b7/uzZszN79uw89thjefHFF3PLLbfU+/q6urp885vfzMiRI5f7/qxZs3LzzTfn5ptvzoknnpgrr7wyVVVVa+pjAAAAAC1Miwko1157bU444YQsWbIkW221VU4++eTsvffe6dChQ/7+979n2rRpue2227LhhhuudI0f/vCHlXiy++6758wzz8yOO+6YadOm5cILL8ykSZMycuTIdOzYMeeee+7a+mgAAABAM9ciAsrkyZNz4oknZsmSJdlnn31y2223ZdNNN11h3tChQ7No0aJ615g6dWouvPDCJEnv3r0zfvz4tG3bNknSp0+fHHbYYRkwYEAmTpyYCy64ICeccEJ23HHHNfehAAAAgBajRdwDZejQoVm4cGG23HLL3HTTTfXGk6Vqamrq/f7w4cNTW1ubJBkxYkQlniy10UYbZcSIEUmS2traXHrppatn8wAAAECL1+wDypQpU3LvvfcmSf7rv/4rW2655SqvUVdXl1tv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09KzZ88kyaWXXprFixevzS0CAAAAzdR6E1BuueWWyviEE06od06rVq3yta99LUny9ttvV4ILAAAAsH5bbwLKgw8+mCRp165d9thjj5XOGzBgQGX80EMPrfF9AQAAAM3fenMPlMmTJydJdtppp1RXr/xj9+jRY4XXNMbMmTMbPD5jxozKePbs2Y1ed11R++6bTb0F1qLSzwPrFj/f6xc/3+sXP9/rFz/f6xc/3+uX9e3ne9m/c9fW1q62davq6urqVttqzdSCBQvStm3bJMkhhxyS22+/vcH57du3z9y5c9OvX788+uijjXqPqqqqT7xPAAAAYPV57LHH0qdPn9Wy1npxCc97771XGbdv3744v127dkniUcYAAABAkvXkEp4FCxZUxjU1NcX5rVu3TpLMnz+/0e+x7CU6K9vDlClTsvXWW6djx44NXkZEyzd79uz07ds3yYfFc5tttmniHQGri59vWHf5+YZ1l5/v9UttbW3eeOONJMluu+222tZdL/4W36ZNm8p40aJFxfkLFy5MksplP43RuXPn4pyddtqp0eux7thmm20a9c8H0PL4+YZ1l59vWHf5+V4/dO3adbWvuV5cwrPxxhtXxo25LGfu3LlJGne5DwAAALDuWy8CSps2bbLlllsmKd99+O23364ElC5duqzxvQEAAADN33oRUJKkZ8+eSZKpU6c2+BijKVOmrPAaAAAAYP223gSUvffeO8mHl+c88cQTK533wAMPVMb9+/df4/sCAAAAmr/1JqD8+7//e2X8m9/8pt45S5YsybXXXpsk2WyzzbLffvutja0BAAAAzdx6E1D69u2bffbZJ0kyevToPProoyvMufjiizN58uQkySmnnJINN9xwre4RAAAAaJ7Wi8cYL3XZZZelf//+mT9/fg488MD8n//zf7Lffvtl/vz5+cMf/pCRI0cmSbp3757TTjutiXcLAAAANBdVdXV1dU29ibXptttuy7HHHpt333233uPdu3fP2LFjs9NOO63lnQEAAADN1XoXUJLklVdeyWWXXZaxY8dm5syZqampyU477ZSjjjoq//Vf/5WNNtqoqbcIAAAANCPrZUABAAAAWBXrzU1kAQAAAD4uAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQXWgIceeihVVVWVX+PHj2/qLQEf0/3337/cz/NHf7Vv3z7du3fPcccdl/vvv7+ptwt8TIsXL84f/vCHHHfccenZs2e22GKLbLjhhtlyyy2zxx575OSTT84999yTJUuWNPVWgQas7M/t6urqdOjQId26dctnP/vZnHrqqfnTn/6URYsWNfWWaUGq6urq6pp6E7CuOfHEE/PrX/+68vWQIUMyatSoJtwR8HHdf//92W+//Ro9/+tf/3pGjhyZDTbYYA3uClidbr311nz3u9/NSy+9VJzbvXv3XHLJJTnkkEPWws6AVbWqf2537Ngx3/nOd/L9738/1dXVa3BnrAsEFFjNFi5cmE996lN555130r59+7z//vvZZJNN8ve//z1t27Zt6u0Bq2jZ/xA7+eST861vfatyrK6uLm+99VYeffTRDB8+PHPmzEmSnHXWWTnnnHOaZL/AqvnZz36WH/zgB1n6n8T7779/Bg0alF69emWzzTbLW2+9leeffz633XZb7r777ixZsiSf+cxn8te//rVpNw7Uq6E/t99///28/fbbefrpp3Pvvffmnnvuqfzs9+3bN7fffns6duzYJPumZRBQYDW74YYb8uUvfzlJMnr06AwZMiRJMmbMmAwePLgptwZ8DMv+h9jZZ5+dH//4x/XOe+6559K7d+/Mnz8/m2yySd58881suOGGa3GnwKq67rrr8rWvfS3Jh/8X+vrrr2/w/1w/88wzGTZsWP7xj38IKNBMNfbP7ST529/+lq9+9auZNGlSkmTvvffOvffem5qamrWxVVog90CB1eyaa65JkvTq1Stf//rX06tXryTJtdde25TbAtawXr16VU7pf/fddzN58uQm3hHQkNdeey0nn3xykmSjjTZq1Gn/u+22W+6+++6cfvrpa2OLwBq266675uGHH87uu++e5MP7GF5xxRVNvCuaMwEFVqM5c+bkrrvuSpIce+yxSZJjjjkmSXLXXXfl9ddfb7K9AWte165dK+MFCxY03UaAouHDh2fu3LlJknPOOafyPzxKWrVqVfkzHmj52rZtm+uuuy5VVVVJkosuuiiLFy9u4l3RXAkosBr97ne/S21tbaqqqirh5JhjjklVVVU++OCD/O53v2viHQJr0vTp0yvj7bbbruk2AjSorq6ucsZou3btcuKJJzbxjoCmtOuuu+aAAw5IksyaNSuPP/54E++I5kpAgdVo6X+M7bPPPpW/PG2//fbZe++9k7iMB9ZlU6ZMydixY5Mkffr0yac+9akm3hGwMs8991zeeOONJB/+mb3JJps08Y6Aprb//vtXxg8++GAT7oTmzHOaYDV55pln8tRTTyXJCqf2HnvssXnwwQfz1FNP5Zlnnsluu+3WFFsEPqE5c+bk2WefrXxdV1eXd955p/IUnqU3kL300kubbpNA0dI/r5PkX//1X5twJ0Bzsey/C1544YUm3AnNmYACq8nSs09at26do446arljRx99dL7zne9k4cKFueaaa3LRRRc1xRaBT+hXv/pVfvWrX9V7rFWrVjnppJMybNiw9OjRYy3vDFgVb775ZmW89dZbN+FOgOZiiy22qIzffvvtJtwJzZlLeGA1+OCDD/L73/8+SXLIIYdks802W+74ZpttloEDByZJfv/73+eDDz5Y21sE1rAlS5bkhhtuyKhRo7Jo0aKm3g7QgPfee68ybteuXRPuBGgu2rdvXxkv++8IWJaAAqvBXXfdldmzZydZ8fKdpZZ+f/bs2bnnnnvW2t6A1efss89OXV3dcr/mzZuXp59+OmeccUbee++9XHzxxTnwwAMzf/78pt4usBIbb7xxZbz0STzA+m3ZaOK+SKyMgAKrwdKbw2622WY55JBD6p2z7JkpbiYL6462bdtmt912y4UXXpgrrrgiSfLAAw/kZz/7WRPvDFiZLbfcsjJ+/fXXm3AnQHOx7KV9HTp0aMKd0JwJKPAJvfvuu7n11luTJO+8805at26dqqqqFX61adMm77zzTpLklltucWogrIOGDBlS+Y+u0aNHN/FugJX5zGc+Uxk/+eSTTbgToLmYNGlSZbzLLrs04U5ozgQU+IRuuOGGVT5Vf968ebnxxhvX0I6AptKqVavsvPPOSZLXXnstb731VhPvCKhPr169KmehPPjgg3n33XebeEdAU7v77rsr47333rsJd0Jz5ik88AktvRxnm222ySWXXFKc/73vfS+vvvpqrr322pxwwglrenvAWlZbW1sZL168uAl3AqxMVVVVjj/++Fx00UWZO3duRo0ale9+97tNvS2giTz77LO59957kyRdunRJ7969m3hHNFcCCnwCL7/8ch566KEkyZFHHpnBgwcXXzNx4sRcfPHFeeCBB/Lqq69mu+22W9PbBNaSefPm5bnnnkuStGnTZrn7LADNy7Bhw3LFFVdk3rx5OeusszJw4MBGPYJ8yZIl+f3vf7/Sm8YDLcv8+fPzta99LXV1dUmS008/PdXV/ppM/VzCA5/AddddV/mX7Ze+9KVGvWbpvLq6ulx33XVrbG/A2nf22WdXLuk76KCDssEGGzTxjoCV2XbbbfPLX/4yyYdP4hkwYEAeeOCBBl/z3HPP5aCDDspFF120NrYIrGHPPfdc9t5778r9TwYMGJCTTz65iXdFcyatwSewNIBstdVW2WeffRr1mj333DOdO3fOzJkzc9111+UHP/jBmtwisBrNmTMnzz777HLfW7BgQV588cVce+21GTduXJIPzz75yU9+0hRbBFbBCSeckJkzZ+ass87KnDlzsu++++bAAw/MoEGD0rNnz2y22WZ566238sILL2Ts2LEZN25cPvjgg+VuQgs0Xx/9c3vu3Ll5++238/TTT+fee+/N3XffXfmfof369cuNN96YDTfcsKm2SwtQVbf0nxhglTz88MOVG0yddNJJufLKKxv92lNOOSW/+MUvkiQTJkzInnvuuUb2CHxy999/f/bbb79Gz+/YsWN++9vf5sADD1yDuwJWp5tuuimnnXZapk+fXpy766675pJLLvEzDs3Ux/lze9iwYTnzzDNdukORf0LgY1p689jkw/ufrIojjzyyElCuvfZaAQVasJqamnTo0CG77rprBg4cmBNOOCGbb755U28LWAVHHHFEDj300Nx4442588478/jjj2fOnDl57733sskmm6Rr167p169fjjzyyOy3336pqqpq6i0Dq6hVq1bZeOONs+mmm2b77bfPHnvskX322SeHHnpoampqmnp7tBDOQAEAAAAocBNZAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACgQUAAAAgAIBBQAAAKBAQAEAAAAoEFAAAAAACgQUAIDV4P77709VVVWqqqpy//33N/V2AIDVTEABAGgh6urq8tBDD+Wss87K5z//+WyzzTapqanJJptskl133TXf+ta38tRTTzX1NgFgnVTd1BsAAKBxunbtmldffXWF7y9evDjPPfdcnnvuuVx55ZU544wzcv7556eqqqoJdgkA6yYBBQCghZg1a1aSZKeddsqRRx6Z/v37p1OnTpk/f37uu+++DB8+PG+//XYuvPDCbLDBBvnpT3/axDsGgHVHVV1dXV1TbwIAoKW7//77s99++yVJ7rvvvuy7776r/T3+7d/+LWeffXYOPPDAes8umTZtWvbaa6+88cYbqa6uzvPPP58ddthhte8DANZH7oECANBCPPLIIznooINWemnOjjvumLPOOitJUltbm1tvvXVtbg8A1mkCCgCw1r355ps544wz0r1797Rt2zZbb711DjjggNx8881JkquvvrryRJvp06cv99quXbumqqoqxx9/fJLkiSeeyPHHH59u3bqldevWK8SFl156KRdffHG++MUvpmvXrmnbtm3atm2b7bffPl/+8pczbty4Ru15/vz5Oe+88/KZz3wm7dq1yxZbbJH+/fvn17/+dZYsWdLoz15XV5cbb7wxRx55ZLp06ZI2bdpk8803T9++ffOTn/wk77zzTqPXqs/Ss2CSD89IAQBWD/dAAQDWqqeeeioHHHBA3njjjcr3FixYkHvuuSf33HNPTjzxxOy1116NWuvKK6/M0KFDU1tbW+/xl19+OTvuuGO9x1599dW8+uqrueGGG3LsscfmN7/5Taqr6/9Po9deey2f//znM2XKlMr35s2bl0ceeSSPPPJIbrrpppx66qnF/b7xxhs5/PDD8/DDDy/3/YULF+bxxx/P448/nssvvzy33npr9txzz+J69Vm4cGFl3KqV/1cGAKuLgAIArDVvv/12vvCFL1TiyTHHHJNjjz02HTt2zNSpU3PZZZdl5MiRjXoU7+OPP57f/va36dKlS04//fTsscce+eCDD/Lggw9W5nzwwQepqanJQQcdlAMOOCC9evVKhw4d8tZbb+WFF17I5Zdfnr/97W/57W9/mx122CHnnHPOCu9TW1ubQw89tBJPDjzwwJx88snp0qVLXn311VxxxRUZN25c/vGPfzS437lz52bAgAGZPHlyampqcsIJJ2TgwIHp0qVL5s6dm/Hjx+eSSy7J66+/noMPPjiTJk3K9ttvvyq/vUmSBx54oDLu0aPHKr8eAKifm8gCAGvNKaeckl/84hdJkosuuiinnXbacsc/+OCDHHnkkcvdu+Pll19O165dK1937do1r7zySpJkt912y/jx47PZZpvV+35z587Nu+++m2222abe43V1dfn617+eq6++Ou3atcusWbOy6aabLjdnxIgR+c53vpMkOfHEE/M///M/K6wzZMiQXHXVVZWv67uJ7NChQ/PLX/4ym266ae6555707t17hXVeeeWV7LXXXpk9e3aOPfbYXHfddfXue2XmzZuXnj175tVXX01NTU1eeumlbLvttqu0BgBQP+d1AgBrxYIFC3LNNdckSf71X/813/3ud1eYs8EGG+R//ud/0qZNm0atefnll680niRJu3btVhpPkqSqqioXX3xxNthgg8ydOzf33HPPCnN+9atfJUm23nrrDB8+vN51LrvssnTs2HGl7/Pmm29m1KhRSZL//u//rjeeJMn222+fH/3oR0mS66+/PvPmzVvpmvX53ve+l1dffTVJ8u1vf1s8AYDVSEABANaKJ554Iv/85z+TJF/72tdW+iSZrbfeOgcddFBxvS5dumSfffZZpT0sXrw4M2fOzOTJk/Pss8/m2WefzWuvvZYtttgiSVa4dOi1117L5MmTkyRHH310Ntpoo3rXbd++fY4++uiVvu+f//znLFiwoLJOQz772c9W9vrEE0807oMl+d3vfpdf/vKXSZKePXvmvPPOa/RrAYAy90ABANaKZ599tjLeY489Gpzbu3fv4iN4P/3pTzfqfRcvXpyRI0fmuuuuy6RJk7Jo0aKVzn3zzTeX+/qZZ56pjPv06dPg+/Tt2zeXX355vccmTpxYGTd0RsxH/f3vf2/UvPvvvz9DhgxJkmy++ea58cYb07Zt20a/DwBQJqAAAGvF22+/XRlvtdVWDc5t6HKYpTbffPPinLfeeisHHnhgo8/kmD9//nJfr8qet95665UemzNnTqPe/6MacwnPxIkTc9hhh2XhwoVp165d7rjjjvTq1etjvR8AsHICCgDQIm2wwQbFOaecckolnvz7v/97vv71r+fTn/50ttpqq7Rp06ZyGdF2222XGTNm5KP31l/265VdclTf3I/64IMPkiQ1NTWrdFlO586dGzz+t7/9LV/4whfy3nvvpXXr1rnlllvSr1+/Rq8PADSegAIArBXLnjEyZ86cdO/efaVzlz7m+JN49913c/311ydJ/uM//iO/+93vVjp32TNNltWhQ4fK+PXXX2/w/Ro6y2TpPVYWLVqULbbYYpUu41mZadOm5YADDsg//vGPVFdX5/rrr8/+++//idcFAOrnJrIAwFqx6667VsbL3hOkPqXjjfHiiy9m8eLFSZLBgwevdN7zzz+f999/v95ju+22W2X8+OOPN/h+DR3ffffdK+O77rqrwXUaY+bMmfn85z+f2bNnp1WrVrnmmmsyaNCgT7wuALByAgoAsFb07t07m266aZLkuuuuW+klL6+//nr+/Oc/f+L3q62trYwbupfIlVdeudJjnTp1Ss+ePZMkf/zjH1e4R8pSc+fOzQ033LDSdQ4++OBsuOGGSZLhw4cvt7dVNWfOnOy///555ZVXkny4///4j//42OsBAI0joAAAa0WbNm3yta99LUny5JNP5pJLLllhzpIlS3LSSSdVHvn7Sey0006V+5Zce+219c65/fbbM2LEiAbXOfnkk5N8+ESc0047rd45p556aoOX8Gy77bY54YQTknz4qOSTTjqpwYgyZ86cjBo1aoXvv/POOznooIPy/PPPJ/kwxnzjG99ocP8AwOpRVdfQHc8AAFajt956K7vuumvl8bzHHHNMvvrVr6Zjx46ZOnVqLrvssjzyyCPp27dvHnvssSTJ9OnTs/3221fW6Nq1a1555ZUcd9xxufrqqxt8v0MPPTRjx45Nkhx00EE56aSTst1222XOnDn505/+lKuvvjo77LBD3nnnnbzxxhv1rllbW5u+fftm0qRJSZIvfOEL+eY3v5kuXbpkxowZueKKK3LXXXelT58+lct47rvvvuy7777LrfP+++9nr732qjzOuVevXjnxxBOzxx57pH379nnnnXfyt7/9Lffcc0/uuOOO7LbbbstdyrRw4cJ87nOfyyOPPFL5vfv+97/f4Odv165dunXr1uAcAKBxBBQAYK166qmncsABB6z0RrHHH3989tlnnwwZMiTJh2d+LPuI4FUJKDNmzMjee++dV199td7j2223Xe68884MHDiwwTVfe+21fO5zn6uc+fFRBx54YE477bQcdNBBSeoPKMmHAemYY47JuHHjGtx3kuy33375y1/+Uvl6+vTpqxxDBgwYkPvvv3+VXgMA1M8lPADAWvWZz3wmzz33XE477bTsvPPOad26dbbccsvst99++f3vf5/f/OY3effddyvzl9435ePo0qVLnnzyyZxxxhnp3r17WrdunU033TSf+cxncvbZZ+evf/1revXqVVynU6dOmTRpUs4999z8r//1v9K2bdtsttlm6devX6644orceeedqampKa7ToUOH3Hnnnbn33ntzwgknZOedd0779u1TXV2dDh06pE+fPvn2t7+dO+64I3fffffH/twAwOrnDBQAoNn5z//8z4wePTqdO3fOjBkzmno7AADOQAEAmpf58+fn1ltvTZL069eviXcDAPAhAQUAWKumTZu20kcYf/DBBzn55JPz5ptvJkmOO+64tbk1AICVcgkPALBWHX/88XnssccyePDg7Lnnntlqq60yf/78PP300/n1r3+dJ598Mkny+c9/PnfffXflUcQAAE2puqk3AACsfyZPnpyzzz57pcf79++f66+/XjwBAJoNZ6AAAGvV888/nz/96U+5++6788orr+SNN97I4sWLs8UWW6R379758pe/nMGDB6dVK1caAwDNh4ACAAAAUOB/7QAAAAAUCCgAAAAABQIKAAAAQIGAAgAAAFAgoAAAAAAUCCgAAAAABQIKAAAAQIGAAgAAAFAgoAAAAAAUCCgAAAAABQIKAAAAQIGAAgAAAFAgoAAAAAAUCCgAAAAABQIKAAAAQIGAAgAAAFAgoAAAAAAUCCgAAAAABf8PSKBmFNf9/jwAAAAASUVORK5CYII="/>


### [Do it! 실습] 목록에 해당하는 행으로 변수 만들기(128쪽)



```python
mpg['size'] = np.where((mpg['category'] == 'compact') |
                       (mpg['category'] == 'subcompact') |
                       (mpg['category'] == '2seater'),
                       'small', 'large')
mpg['size'].value_counts()
```

<pre>
size
large    147
small     87
Name: count, dtype: int64
</pre>

```python
# np.where() -> df.isin()

mpg['size'] = np.where(mpg['category'].isin(['compact', 'subcompact', '2seater']), 'small', 'large')
mpg['size'].value_counts()
```

<pre>
size
large    147
small     87
Name: count, dtype: int64
</pre>

### [분석 도전]

- midwest.csv는 미국 동북중부(East North Central States) 437개 지역의 인구통계 정보를 담고 있습니다. midwest.csv를 이용해 데이터 분석 문제를 해결해 보세요.

- midwest 데이터 출처: bit.ly/easypy_52


#### 문제1

- midwest.csv를 불러와 데이터의 특징을 파악하세요



```python
midwest = pd.read_csv('midwest.csv')
midwest
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>PID</th>
      <th>county</th>
      <th>state</th>
      <th>area</th>
      <th>poptotal</th>
      <th>popdensity</th>
      <th>popwhite</th>
      <th>popblack</th>
      <th>popamerindian</th>
      <th>popasian</th>
      <th>...</th>
      <th>percollege</th>
      <th>percprof</th>
      <th>poppovertyknown</th>
      <th>percpovertyknown</th>
      <th>percbelowpoverty</th>
      <th>percchildbelowpovert</th>
      <th>percadultpoverty</th>
      <th>percelderlypoverty</th>
      <th>inmetro</th>
      <th>category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>561</td>
      <td>ADAMS</td>
      <td>IL</td>
      <td>0.052</td>
      <td>66090</td>
      <td>1270.961540</td>
      <td>63917</td>
      <td>1702</td>
      <td>98</td>
      <td>249</td>
      <td>...</td>
      <td>19.631392</td>
      <td>4.355859</td>
      <td>63628</td>
      <td>96.274777</td>
      <td>13.151443</td>
      <td>18.011717</td>
      <td>11.009776</td>
      <td>12.443812</td>
      <td>0</td>
      <td>AAR</td>
    </tr>
    <tr>
      <th>1</th>
      <td>562</td>
      <td>ALEXANDER</td>
      <td>IL</td>
      <td>0.014</td>
      <td>10626</td>
      <td>759.000000</td>
      <td>7054</td>
      <td>3496</td>
      <td>19</td>
      <td>48</td>
      <td>...</td>
      <td>11.243308</td>
      <td>2.870315</td>
      <td>10529</td>
      <td>99.087145</td>
      <td>32.244278</td>
      <td>45.826514</td>
      <td>27.385647</td>
      <td>25.228976</td>
      <td>0</td>
      <td>LHR</td>
    </tr>
    <tr>
      <th>2</th>
      <td>563</td>
      <td>BOND</td>
      <td>IL</td>
      <td>0.022</td>
      <td>14991</td>
      <td>681.409091</td>
      <td>14477</td>
      <td>429</td>
      <td>35</td>
      <td>16</td>
      <td>...</td>
      <td>17.033819</td>
      <td>4.488572</td>
      <td>14235</td>
      <td>94.956974</td>
      <td>12.068844</td>
      <td>14.036061</td>
      <td>10.852090</td>
      <td>12.697410</td>
      <td>0</td>
      <td>AAR</td>
    </tr>
    <tr>
      <th>3</th>
      <td>564</td>
      <td>BOONE</td>
      <td>IL</td>
      <td>0.017</td>
      <td>30806</td>
      <td>1812.117650</td>
      <td>29344</td>
      <td>127</td>
      <td>46</td>
      <td>150</td>
      <td>...</td>
      <td>17.278954</td>
      <td>4.197800</td>
      <td>30337</td>
      <td>98.477569</td>
      <td>7.209019</td>
      <td>11.179536</td>
      <td>5.536013</td>
      <td>6.217047</td>
      <td>1</td>
      <td>ALU</td>
    </tr>
    <tr>
      <th>4</th>
      <td>565</td>
      <td>BROWN</td>
      <td>IL</td>
      <td>0.018</td>
      <td>5836</td>
      <td>324.222222</td>
      <td>5264</td>
      <td>547</td>
      <td>14</td>
      <td>5</td>
      <td>...</td>
      <td>14.475999</td>
      <td>3.367680</td>
      <td>4815</td>
      <td>82.505140</td>
      <td>13.520249</td>
      <td>13.022889</td>
      <td>11.143211</td>
      <td>19.200000</td>
      <td>0</td>
      <td>AAR</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>432</th>
      <td>3048</td>
      <td>WAUKESHA</td>
      <td>WI</td>
      <td>0.034</td>
      <td>304715</td>
      <td>8962.205880</td>
      <td>298313</td>
      <td>1096</td>
      <td>672</td>
      <td>2699</td>
      <td>...</td>
      <td>35.396784</td>
      <td>7.667090</td>
      <td>299802</td>
      <td>98.387674</td>
      <td>3.121060</td>
      <td>3.785820</td>
      <td>2.590061</td>
      <td>4.085479</td>
      <td>1</td>
      <td>HLU</td>
    </tr>
    <tr>
      <th>433</th>
      <td>3049</td>
      <td>WAUPACA</td>
      <td>WI</td>
      <td>0.045</td>
      <td>46104</td>
      <td>1024.533330</td>
      <td>45695</td>
      <td>22</td>
      <td>125</td>
      <td>92</td>
      <td>...</td>
      <td>16.549869</td>
      <td>3.138596</td>
      <td>44412</td>
      <td>96.330036</td>
      <td>8.488697</td>
      <td>10.071411</td>
      <td>6.953799</td>
      <td>10.338641</td>
      <td>0</td>
      <td>AAR</td>
    </tr>
    <tr>
      <th>434</th>
      <td>3050</td>
      <td>WAUSHARA</td>
      <td>WI</td>
      <td>0.037</td>
      <td>19385</td>
      <td>523.918919</td>
      <td>19094</td>
      <td>29</td>
      <td>70</td>
      <td>43</td>
      <td>...</td>
      <td>15.064584</td>
      <td>2.620907</td>
      <td>19163</td>
      <td>98.854785</td>
      <td>13.786985</td>
      <td>20.050708</td>
      <td>11.695784</td>
      <td>11.804558</td>
      <td>0</td>
      <td>AAR</td>
    </tr>
    <tr>
      <th>435</th>
      <td>3051</td>
      <td>WINNEBAGO</td>
      <td>WI</td>
      <td>0.035</td>
      <td>140320</td>
      <td>4009.142860</td>
      <td>136822</td>
      <td>697</td>
      <td>685</td>
      <td>1728</td>
      <td>...</td>
      <td>24.995504</td>
      <td>5.659847</td>
      <td>133950</td>
      <td>95.460376</td>
      <td>8.804031</td>
      <td>10.592031</td>
      <td>8.660587</td>
      <td>6.661094</td>
      <td>1</td>
      <td>HAU</td>
    </tr>
    <tr>
      <th>436</th>
      <td>3052</td>
      <td>WOOD</td>
      <td>WI</td>
      <td>0.048</td>
      <td>73605</td>
      <td>1533.437500</td>
      <td>72157</td>
      <td>90</td>
      <td>481</td>
      <td>722</td>
      <td>...</td>
      <td>21.666382</td>
      <td>4.583725</td>
      <td>72685</td>
      <td>98.750085</td>
      <td>8.525831</td>
      <td>11.162997</td>
      <td>7.375656</td>
      <td>7.882918</td>
      <td>0</td>
      <td>AAR</td>
    </tr>
  </tbody>
</table>
<p>437 rows × 28 columns</p>
</div>



```python
midwest.shape
```

<pre>
(437, 28)
</pre>

```python
midwest.columns
```

<pre>
Index(['PID', 'county', 'state', 'area', 'poptotal', 'popdensity', 'popwhite',
       'popblack', 'popamerindian', 'popasian', 'popother', 'percwhite',
       'percblack', 'percamerindan', 'percasian', 'percother', 'popadults',
       'perchsd', 'percollege', 'percprof', 'poppovertyknown',
       'percpovertyknown', 'percbelowpoverty', 'percchildbelowpovert',
       'percadultpoverty', 'percelderlypoverty', 'inmetro', 'category'],
      dtype='object')
</pre>

```python
midwest.describe()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>PID</th>
      <th>area</th>
      <th>poptotal</th>
      <th>popdensity</th>
      <th>popwhite</th>
      <th>popblack</th>
      <th>popamerindian</th>
      <th>popasian</th>
      <th>popother</th>
      <th>percwhite</th>
      <th>...</th>
      <th>perchsd</th>
      <th>percollege</th>
      <th>percprof</th>
      <th>poppovertyknown</th>
      <th>percpovertyknown</th>
      <th>percbelowpoverty</th>
      <th>percchildbelowpovert</th>
      <th>percadultpoverty</th>
      <th>percelderlypoverty</th>
      <th>inmetro</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>437.000000</td>
      <td>437.000000</td>
      <td>4.370000e+02</td>
      <td>437.000000</td>
      <td>4.370000e+02</td>
      <td>4.370000e+02</td>
      <td>437.000000</td>
      <td>437.000000</td>
      <td>437.000000</td>
      <td>437.000000</td>
      <td>...</td>
      <td>437.000000</td>
      <td>437.000000</td>
      <td>437.000000</td>
      <td>4.370000e+02</td>
      <td>437.000000</td>
      <td>437.000000</td>
      <td>437.000000</td>
      <td>437.000000</td>
      <td>437.000000</td>
      <td>437.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>1437.338673</td>
      <td>0.033169</td>
      <td>9.613030e+04</td>
      <td>3097.742985</td>
      <td>8.183992e+04</td>
      <td>1.102388e+04</td>
      <td>343.109840</td>
      <td>1310.464531</td>
      <td>1612.931350</td>
      <td>95.558441</td>
      <td>...</td>
      <td>73.965546</td>
      <td>18.272736</td>
      <td>4.447259</td>
      <td>9.364228e+04</td>
      <td>97.110267</td>
      <td>12.510505</td>
      <td>16.447464</td>
      <td>10.918798</td>
      <td>11.389043</td>
      <td>0.343249</td>
    </tr>
    <tr>
      <th>std</th>
      <td>876.390266</td>
      <td>0.014679</td>
      <td>2.981705e+05</td>
      <td>7664.751786</td>
      <td>2.001966e+05</td>
      <td>7.895827e+04</td>
      <td>868.926751</td>
      <td>9518.394189</td>
      <td>18526.540699</td>
      <td>7.087358</td>
      <td>...</td>
      <td>5.843177</td>
      <td>6.261908</td>
      <td>2.408427</td>
      <td>2.932351e+05</td>
      <td>2.749863</td>
      <td>5.150155</td>
      <td>7.228634</td>
      <td>5.109166</td>
      <td>3.661259</td>
      <td>0.475338</td>
    </tr>
    <tr>
      <th>min</th>
      <td>561.000000</td>
      <td>0.005000</td>
      <td>1.701000e+03</td>
      <td>85.050000</td>
      <td>4.160000e+02</td>
      <td>0.000000e+00</td>
      <td>4.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>10.694087</td>
      <td>...</td>
      <td>46.912261</td>
      <td>7.336108</td>
      <td>0.520291</td>
      <td>1.696000e+03</td>
      <td>80.902441</td>
      <td>2.180168</td>
      <td>1.918955</td>
      <td>1.938504</td>
      <td>3.547067</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>670.000000</td>
      <td>0.024000</td>
      <td>1.884000e+04</td>
      <td>622.407407</td>
      <td>1.863000e+04</td>
      <td>2.900000e+01</td>
      <td>44.000000</td>
      <td>35.000000</td>
      <td>20.000000</td>
      <td>94.886032</td>
      <td>...</td>
      <td>71.325329</td>
      <td>14.113725</td>
      <td>2.997957</td>
      <td>1.836400e+04</td>
      <td>96.894572</td>
      <td>9.198715</td>
      <td>11.624088</td>
      <td>7.668009</td>
      <td>8.911763</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1221.000000</td>
      <td>0.030000</td>
      <td>3.532400e+04</td>
      <td>1156.208330</td>
      <td>3.447100e+04</td>
      <td>2.010000e+02</td>
      <td>94.000000</td>
      <td>102.000000</td>
      <td>66.000000</td>
      <td>98.032742</td>
      <td>...</td>
      <td>74.246891</td>
      <td>16.797562</td>
      <td>3.814239</td>
      <td>3.378800e+04</td>
      <td>98.169562</td>
      <td>11.822313</td>
      <td>15.270164</td>
      <td>10.007610</td>
      <td>10.869119</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>2059.000000</td>
      <td>0.038000</td>
      <td>7.565100e+04</td>
      <td>2330.000000</td>
      <td>7.296800e+04</td>
      <td>1.291000e+03</td>
      <td>288.000000</td>
      <td>401.000000</td>
      <td>345.000000</td>
      <td>99.074935</td>
      <td>...</td>
      <td>77.195345</td>
      <td>20.549893</td>
      <td>4.949324</td>
      <td>7.284000e+04</td>
      <td>98.598636</td>
      <td>15.133226</td>
      <td>20.351878</td>
      <td>13.182182</td>
      <td>13.412162</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>3052.000000</td>
      <td>0.110000</td>
      <td>5.105067e+06</td>
      <td>88018.396600</td>
      <td>3.204947e+06</td>
      <td>1.317147e+06</td>
      <td>10289.000000</td>
      <td>188565.000000</td>
      <td>384119.000000</td>
      <td>99.822821</td>
      <td>...</td>
      <td>88.898674</td>
      <td>48.078510</td>
      <td>20.791321</td>
      <td>5.023523e+06</td>
      <td>99.860384</td>
      <td>48.691099</td>
      <td>64.308477</td>
      <td>43.312464</td>
      <td>31.161972</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
<p>8 rows × 25 columns</p>
</div>


#### 문제2

- poptotal(전체 인구) 변수를 total로, popasian(아시아 인구) 변수를 asian으로 수정하세요.



```python
midwest_new = midwest.copy()
```


```python
midwest_new = midwest_new.rename(columns = {'poptotal':'total', 
                                            'popasian' : 'asian'},
                                 )
midwest_new
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>PID</th>
      <th>county</th>
      <th>state</th>
      <th>area</th>
      <th>total</th>
      <th>popdensity</th>
      <th>popwhite</th>
      <th>popblack</th>
      <th>popamerindian</th>
      <th>asian</th>
      <th>...</th>
      <th>percollege</th>
      <th>percprof</th>
      <th>poppovertyknown</th>
      <th>percpovertyknown</th>
      <th>percbelowpoverty</th>
      <th>percchildbelowpovert</th>
      <th>percadultpoverty</th>
      <th>percelderlypoverty</th>
      <th>inmetro</th>
      <th>category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>561</td>
      <td>ADAMS</td>
      <td>IL</td>
      <td>0.052</td>
      <td>66090</td>
      <td>1270.961540</td>
      <td>63917</td>
      <td>1702</td>
      <td>98</td>
      <td>249</td>
      <td>...</td>
      <td>19.631392</td>
      <td>4.355859</td>
      <td>63628</td>
      <td>96.274777</td>
      <td>13.151443</td>
      <td>18.011717</td>
      <td>11.009776</td>
      <td>12.443812</td>
      <td>0</td>
      <td>AAR</td>
    </tr>
    <tr>
      <th>1</th>
      <td>562</td>
      <td>ALEXANDER</td>
      <td>IL</td>
      <td>0.014</td>
      <td>10626</td>
      <td>759.000000</td>
      <td>7054</td>
      <td>3496</td>
      <td>19</td>
      <td>48</td>
      <td>...</td>
      <td>11.243308</td>
      <td>2.870315</td>
      <td>10529</td>
      <td>99.087145</td>
      <td>32.244278</td>
      <td>45.826514</td>
      <td>27.385647</td>
      <td>25.228976</td>
      <td>0</td>
      <td>LHR</td>
    </tr>
    <tr>
      <th>2</th>
      <td>563</td>
      <td>BOND</td>
      <td>IL</td>
      <td>0.022</td>
      <td>14991</td>
      <td>681.409091</td>
      <td>14477</td>
      <td>429</td>
      <td>35</td>
      <td>16</td>
      <td>...</td>
      <td>17.033819</td>
      <td>4.488572</td>
      <td>14235</td>
      <td>94.956974</td>
      <td>12.068844</td>
      <td>14.036061</td>
      <td>10.852090</td>
      <td>12.697410</td>
      <td>0</td>
      <td>AAR</td>
    </tr>
    <tr>
      <th>3</th>
      <td>564</td>
      <td>BOONE</td>
      <td>IL</td>
      <td>0.017</td>
      <td>30806</td>
      <td>1812.117650</td>
      <td>29344</td>
      <td>127</td>
      <td>46</td>
      <td>150</td>
      <td>...</td>
      <td>17.278954</td>
      <td>4.197800</td>
      <td>30337</td>
      <td>98.477569</td>
      <td>7.209019</td>
      <td>11.179536</td>
      <td>5.536013</td>
      <td>6.217047</td>
      <td>1</td>
      <td>ALU</td>
    </tr>
    <tr>
      <th>4</th>
      <td>565</td>
      <td>BROWN</td>
      <td>IL</td>
      <td>0.018</td>
      <td>5836</td>
      <td>324.222222</td>
      <td>5264</td>
      <td>547</td>
      <td>14</td>
      <td>5</td>
      <td>...</td>
      <td>14.475999</td>
      <td>3.367680</td>
      <td>4815</td>
      <td>82.505140</td>
      <td>13.520249</td>
      <td>13.022889</td>
      <td>11.143211</td>
      <td>19.200000</td>
      <td>0</td>
      <td>AAR</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>432</th>
      <td>3048</td>
      <td>WAUKESHA</td>
      <td>WI</td>
      <td>0.034</td>
      <td>304715</td>
      <td>8962.205880</td>
      <td>298313</td>
      <td>1096</td>
      <td>672</td>
      <td>2699</td>
      <td>...</td>
      <td>35.396784</td>
      <td>7.667090</td>
      <td>299802</td>
      <td>98.387674</td>
      <td>3.121060</td>
      <td>3.785820</td>
      <td>2.590061</td>
      <td>4.085479</td>
      <td>1</td>
      <td>HLU</td>
    </tr>
    <tr>
      <th>433</th>
      <td>3049</td>
      <td>WAUPACA</td>
      <td>WI</td>
      <td>0.045</td>
      <td>46104</td>
      <td>1024.533330</td>
      <td>45695</td>
      <td>22</td>
      <td>125</td>
      <td>92</td>
      <td>...</td>
      <td>16.549869</td>
      <td>3.138596</td>
      <td>44412</td>
      <td>96.330036</td>
      <td>8.488697</td>
      <td>10.071411</td>
      <td>6.953799</td>
      <td>10.338641</td>
      <td>0</td>
      <td>AAR</td>
    </tr>
    <tr>
      <th>434</th>
      <td>3050</td>
      <td>WAUSHARA</td>
      <td>WI</td>
      <td>0.037</td>
      <td>19385</td>
      <td>523.918919</td>
      <td>19094</td>
      <td>29</td>
      <td>70</td>
      <td>43</td>
      <td>...</td>
      <td>15.064584</td>
      <td>2.620907</td>
      <td>19163</td>
      <td>98.854785</td>
      <td>13.786985</td>
      <td>20.050708</td>
      <td>11.695784</td>
      <td>11.804558</td>
      <td>0</td>
      <td>AAR</td>
    </tr>
    <tr>
      <th>435</th>
      <td>3051</td>
      <td>WINNEBAGO</td>
      <td>WI</td>
      <td>0.035</td>
      <td>140320</td>
      <td>4009.142860</td>
      <td>136822</td>
      <td>697</td>
      <td>685</td>
      <td>1728</td>
      <td>...</td>
      <td>24.995504</td>
      <td>5.659847</td>
      <td>133950</td>
      <td>95.460376</td>
      <td>8.804031</td>
      <td>10.592031</td>
      <td>8.660587</td>
      <td>6.661094</td>
      <td>1</td>
      <td>HAU</td>
    </tr>
    <tr>
      <th>436</th>
      <td>3052</td>
      <td>WOOD</td>
      <td>WI</td>
      <td>0.048</td>
      <td>73605</td>
      <td>1533.437500</td>
      <td>72157</td>
      <td>90</td>
      <td>481</td>
      <td>722</td>
      <td>...</td>
      <td>21.666382</td>
      <td>4.583725</td>
      <td>72685</td>
      <td>98.750085</td>
      <td>8.525831</td>
      <td>11.162997</td>
      <td>7.375656</td>
      <td>7.882918</td>
      <td>0</td>
      <td>AAR</td>
    </tr>
  </tbody>
</table>
<p>437 rows × 28 columns</p>
</div>


#### 문제3

- total, asian 변수를 이용해 '전체 인구 대비 아시아 인구 백분율' 파생변수를 추가하고, 히스토그램을 만들어 분포를 살펴보세요.



```python
midwest_new['asian_percent'] = (midwest_new['asian']/midwest_new['total'])*100
midwest_new
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>PID</th>
      <th>county</th>
      <th>state</th>
      <th>area</th>
      <th>total</th>
      <th>popdensity</th>
      <th>popwhite</th>
      <th>popblack</th>
      <th>popamerindian</th>
      <th>asian</th>
      <th>...</th>
      <th>percprof</th>
      <th>poppovertyknown</th>
      <th>percpovertyknown</th>
      <th>percbelowpoverty</th>
      <th>percchildbelowpovert</th>
      <th>percadultpoverty</th>
      <th>percelderlypoverty</th>
      <th>inmetro</th>
      <th>category</th>
      <th>asian_percent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>561</td>
      <td>ADAMS</td>
      <td>IL</td>
      <td>0.052</td>
      <td>66090</td>
      <td>1270.961540</td>
      <td>63917</td>
      <td>1702</td>
      <td>98</td>
      <td>249</td>
      <td>...</td>
      <td>4.355859</td>
      <td>63628</td>
      <td>96.274777</td>
      <td>13.151443</td>
      <td>18.011717</td>
      <td>11.009776</td>
      <td>12.443812</td>
      <td>0</td>
      <td>AAR</td>
      <td>0.376759</td>
    </tr>
    <tr>
      <th>1</th>
      <td>562</td>
      <td>ALEXANDER</td>
      <td>IL</td>
      <td>0.014</td>
      <td>10626</td>
      <td>759.000000</td>
      <td>7054</td>
      <td>3496</td>
      <td>19</td>
      <td>48</td>
      <td>...</td>
      <td>2.870315</td>
      <td>10529</td>
      <td>99.087145</td>
      <td>32.244278</td>
      <td>45.826514</td>
      <td>27.385647</td>
      <td>25.228976</td>
      <td>0</td>
      <td>LHR</td>
      <td>0.451722</td>
    </tr>
    <tr>
      <th>2</th>
      <td>563</td>
      <td>BOND</td>
      <td>IL</td>
      <td>0.022</td>
      <td>14991</td>
      <td>681.409091</td>
      <td>14477</td>
      <td>429</td>
      <td>35</td>
      <td>16</td>
      <td>...</td>
      <td>4.488572</td>
      <td>14235</td>
      <td>94.956974</td>
      <td>12.068844</td>
      <td>14.036061</td>
      <td>10.852090</td>
      <td>12.697410</td>
      <td>0</td>
      <td>AAR</td>
      <td>0.106731</td>
    </tr>
    <tr>
      <th>3</th>
      <td>564</td>
      <td>BOONE</td>
      <td>IL</td>
      <td>0.017</td>
      <td>30806</td>
      <td>1812.117650</td>
      <td>29344</td>
      <td>127</td>
      <td>46</td>
      <td>150</td>
      <td>...</td>
      <td>4.197800</td>
      <td>30337</td>
      <td>98.477569</td>
      <td>7.209019</td>
      <td>11.179536</td>
      <td>5.536013</td>
      <td>6.217047</td>
      <td>1</td>
      <td>ALU</td>
      <td>0.486918</td>
    </tr>
    <tr>
      <th>4</th>
      <td>565</td>
      <td>BROWN</td>
      <td>IL</td>
      <td>0.018</td>
      <td>5836</td>
      <td>324.222222</td>
      <td>5264</td>
      <td>547</td>
      <td>14</td>
      <td>5</td>
      <td>...</td>
      <td>3.367680</td>
      <td>4815</td>
      <td>82.505140</td>
      <td>13.520249</td>
      <td>13.022889</td>
      <td>11.143211</td>
      <td>19.200000</td>
      <td>0</td>
      <td>AAR</td>
      <td>0.085675</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>432</th>
      <td>3048</td>
      <td>WAUKESHA</td>
      <td>WI</td>
      <td>0.034</td>
      <td>304715</td>
      <td>8962.205880</td>
      <td>298313</td>
      <td>1096</td>
      <td>672</td>
      <td>2699</td>
      <td>...</td>
      <td>7.667090</td>
      <td>299802</td>
      <td>98.387674</td>
      <td>3.121060</td>
      <td>3.785820</td>
      <td>2.590061</td>
      <td>4.085479</td>
      <td>1</td>
      <td>HLU</td>
      <td>0.885746</td>
    </tr>
    <tr>
      <th>433</th>
      <td>3049</td>
      <td>WAUPACA</td>
      <td>WI</td>
      <td>0.045</td>
      <td>46104</td>
      <td>1024.533330</td>
      <td>45695</td>
      <td>22</td>
      <td>125</td>
      <td>92</td>
      <td>...</td>
      <td>3.138596</td>
      <td>44412</td>
      <td>96.330036</td>
      <td>8.488697</td>
      <td>10.071411</td>
      <td>6.953799</td>
      <td>10.338641</td>
      <td>0</td>
      <td>AAR</td>
      <td>0.199549</td>
    </tr>
    <tr>
      <th>434</th>
      <td>3050</td>
      <td>WAUSHARA</td>
      <td>WI</td>
      <td>0.037</td>
      <td>19385</td>
      <td>523.918919</td>
      <td>19094</td>
      <td>29</td>
      <td>70</td>
      <td>43</td>
      <td>...</td>
      <td>2.620907</td>
      <td>19163</td>
      <td>98.854785</td>
      <td>13.786985</td>
      <td>20.050708</td>
      <td>11.695784</td>
      <td>11.804558</td>
      <td>0</td>
      <td>AAR</td>
      <td>0.221821</td>
    </tr>
    <tr>
      <th>435</th>
      <td>3051</td>
      <td>WINNEBAGO</td>
      <td>WI</td>
      <td>0.035</td>
      <td>140320</td>
      <td>4009.142860</td>
      <td>136822</td>
      <td>697</td>
      <td>685</td>
      <td>1728</td>
      <td>...</td>
      <td>5.659847</td>
      <td>133950</td>
      <td>95.460376</td>
      <td>8.804031</td>
      <td>10.592031</td>
      <td>8.660587</td>
      <td>6.661094</td>
      <td>1</td>
      <td>HAU</td>
      <td>1.231471</td>
    </tr>
    <tr>
      <th>436</th>
      <td>3052</td>
      <td>WOOD</td>
      <td>WI</td>
      <td>0.048</td>
      <td>73605</td>
      <td>1533.437500</td>
      <td>72157</td>
      <td>90</td>
      <td>481</td>
      <td>722</td>
      <td>...</td>
      <td>4.583725</td>
      <td>72685</td>
      <td>98.750085</td>
      <td>8.525831</td>
      <td>11.162997</td>
      <td>7.375656</td>
      <td>7.882918</td>
      <td>0</td>
      <td>AAR</td>
      <td>0.980912</td>
    </tr>
  </tbody>
</table>
<p>437 rows × 29 columns</p>
</div>



```python
midwest_new['asian_percent'].sort_values()
```

<pre>
404    0.000000
105    0.010592
109    0.015950
358    0.027032
390    0.032504
         ...   
180    3.691481
15     3.693683
274    4.143679
9      4.642682
21     5.070452
Name: asian_percent, Length: 437, dtype: float64
</pre>

```python
midwest_new['asian_percent'].plot.hist()
```

<pre>
<Axes: ylabel='Frequency'>
</pre>
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABHcAAAM6CAYAAAALzq8nAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjcuMiwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8pXeV/AAAACXBIWXMAAB7CAAAewgFu0HU+AABa+0lEQVR4nO3de5TVdb0//udG4iKo6EFIBMUbgqfON49AIipiYYkkoumxOgpGWJ7yUng7ZabnpHlBwcMqjcTQUryQ2QrKTEXUwhSjtAJ1QBIQQzheGRBG9u8PfuwDAjODwsx84PFYa9Z6z36/P+/92jiLxTx9X0rlcrkcAAAAAAqpWWMXAAAAAMD7J9wBAAAAKDDhDgAAAECBCXcAAAAACky4AwAAAFBgwh0AAACAAhPuAAAAABSYcAcAAACgwIQ7AAAAAAUm3AEAAAAoMOEOAAAAQIEJdwAAAAAKTLgDAAAAUGDCHQAAAIACE+4AAAAAFJhwBwAAAKDAmjd2ATS+FStW5Nlnn02S7L777mne3I8FAAAAbGk1NTV59dVXkyQf/ehH06pVqy0yr9/iybPPPpvevXs3dhkAAACw3XjyySfTq1evLTKXbVkAAAAABWblDtl9990r7SeffDJ77LFHI1YDAAAA26ZFixZVds6s+7v4ByXcYb0zdvbYY4907ty5EasBAACAbd+WPO/WtiwAAACAAhPuAAAAABSYcAcAAACgwIQ7AAAAAAUm3AEAAAAoMOEOAAAAQIEJdwAAAAAKTLgDAAAAUGDCHQAAAIACE+4AAAAAFJhwBwAAAKDAhDsAAAAABSbcAQAAACgw4Q4AAABAgQl3AAAAAApMuAMAAABQYMIdAAAAgAIT7gAAAAAUmHAHAAAAoMCEOwAAAAAFJtwBAAAAKDDhDgAAAECBCXcAAAAACky4AwAAAFBgwh0AAACAAhPuAAAAABSYcAcAAACgwIQ7AAAAAAUm3AEAAAAoMOEOAAAAQIEJdwAAAAAKTLgDAAAAUGDCHQAAAIACa97YBcAH1fXiKY1dwnZh3lXHNXYJAAAAbISVOwAAAAAFJtwBAAAAKDDhDgAAAECBCXcAAAAACky4AwAAAFBgwh0AAACAAhPuAAAAABSYcAcAAACgwIQ7AAAAAAUm3AEAAAAoMOEOAAAAQIEJdwAAAAAKTLgDAAAAUGDCHQAAAIACE+4AAAAAFJhwBwAAAKDAhDsAAAAABSbcAQAAACgw4Q4AAABAgQl3AAAAAApMuAMAAABQYMIdAAAAgAIT7gAAAAAUmHAHAAAAoMCEOwAAAAAFJtwBAAAAKDDhDgAAAECBCXcAAAAACky4AwAAAFBgwh0AAACAAhPuAAAAABSYcAcAAACgwIQ7AAAAAAUm3AEAAAAoMOEOAAAAQIEJdwAAAAAKTLgDAAAAUGDCHQAAAIACE+4AAAAAFJhwBwAAAKDAhDsAAAAABSbcAQAAACgw4Q4AAABAgQl3AAAAAApMuAMAAABQYNtluPPmm2/mzjvvzMiRI9OvX7/sv//+2WWXXdKiRYt06NAhRx11VK655posXbq0XvPdf//9OfHEE9O5c+e0bNkynTt3zoknnpj777+/3jVVV1fn2muvTe/evbPbbrulbdu26dGjR84///y89NJL7/ejAgAAANu4UrlcLjd2EQ3twQcfzIABA+oc1759+/z0pz/Npz71qY32l8vlfOUrX8m4ceM2OceZZ56Zm266KaVSaZNj5syZk+OOOy7PPffcRvt32WWX3HHHHRk4cGCdNb8fCxYsSJcuXZIk8+fPT+fOnbfK+2wtXS+e0tglbBfmXXVcY5cAAABQaFvr9+/tcuVOknTp0iWnn356brjhhtx7772ZPn16fve73+Wuu+7KySefnB122CFLlizJ8ccfn2eeeWajc1xyySWVYOfggw/OxIkT8+STT2bixIk5+OCDkyTjxo3Lt7/97U3W8fbbb2fQoEGVYGfEiBF56KGH8vvf/z5XXHFF2rZtmzfeeCMnn3zyJusAAAAAtl/b5cqdd999NzvssEOtY+67774MGTIkSXLiiSfmZz/72Xr9VVVV6dGjR2pqatKzZ888+uijad26daW/uro6/fr1y4wZM9K8efPMnj07++233wbvc9lll+Xyyy9PklxzzTW54IIL1uufPn16jjzyyNTU1KR///55+OGH39dnro2VO9SHlTsAAAAfjJU7W1BdwU6SnHDCCenevXuS5NFHH92gf/To0ampqUmSjB07dr1gJ0l23HHHjB07NklSU1OTMWPGbDDHqlWrcsMNNyRJevTokZEjR24wpk+fPhk+fHiSZOrUqXn66afrrB0AAADYfmyX4U59tWnTJkmyYsWK9V4vl8v5xS9+kSTp3r17Dj300I0+f+ihh+bAAw9MsmYl0HsXST3yyCN5/fXXkyRDhw5Ns2Yb/88xbNiwSvvee+/d7M8BAAAAbLuEO5swa9as/OlPf0qSygqetV588cUsXLgwSdKvX79a51nbv2DBgsybN2+9vscee2yDcRvTs2fPStD0+OOP16t+AAAAYPsg3FlHdXV1XnjhhVx//fXp379/3n333STJueeeu964WbNmVdrvDX7ea93+dZ/bnHmaN29eOa/nvXMAAAAA27fmjV1AY5swYULOOOOMTfaff/75+cIXvrDea/Pnz6+06zr8aO1BSe99bt3v27Rpk3bt2tU5zzPPPJNXX30177zzTlq2bFnr+HUtWLCg1v5FixbVey4AAACgadnuw51N+djHPpabbropH//4xzfoe+uttyrttm3b1jrP2u1UyZprzzc2T11zbGyezQl31g2YAAAAgG3Ldr8t64QTTsizzz6bZ599Nk8++WQmTpyYIUOG5E9/+lO+8IUvZPLkyRs8s+4Byy1atKh1/nVDmOXLl290nrrmqGseAAAAYPu13a/cadeu3Xpbonr16pVTTz01P/nJTzJ06NAMHjw448ePX+/GqlatWlXaK1eurHX+d955p9J+73Xpa+epa4665qnLe7eDvdeiRYvSu3fvzZoTAAAAaBq2+3BnU0477bRMnjw5d999d772ta9l8ODB2XXXXZMkO+20U2Xce7davdeyZcsq7fduv1o7T11z1DVPXeo6FwgAAAAoru1+W1ZtBg8enGRNsPLrX/+68vq6YUldhxWvu2rmvWffrJ1n2bJlef311+s1z+67775Z5+0AAAAA2zbhTi123333Svvvf/97pX3QQQdV2rNnz651jnX7e/TosV5ffeepqanJnDlzNjoHAAAAsH0T7tRi4cKFlfa6W6H22WefdOrUKUkybdq0Wud49NFHkyR77rlnunbtul7f4YcfXmnXNs+MGTMq27L69u1bv+IBAACA7YJwpxb33HNPpf3Rj3600i6VSpUtW7Nnz84TTzyx0eefeOKJyoqcwYMHp1Qqrdd/1FFHZZdddkmS3HrrrSmXyxudZ8KECZX2kCFDNv+DAAAAANus7TLcmTBhwnrXmW/M6NGj86tf/SpJ0rVr1/VW2STJeeedl+bN15xHffbZZ29wPfny5ctz9tlnJ0maN2+e8847b4P3aNGiRc4555wkyaxZszJq1KgNxkyfPj3j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HQAAAIACE+4AAAAAFJhwBwAAAKDAhDsAAAAABbbdhjt//OMfc+WVV+bYY49Nly5d0rJly7Rt2zbdunXLsGHD8thjj23WfPfff39OPPHEdO7cOS1btkznzp1z4okn5v7776/3HNXV1bn22mvTu3fv7Lbbbmnbtm169OiR888/Py+99NLmfkQAAABgO1Aql8vlxi6iofXr1y+PPvponeNOO+203HzzzWnRosUmx5TL5XzlK1/JuHHjNjnmzDPPzE033ZRSqbTJMXPmzMlxxx2X5557bqP9u+yyS+64444MHDiwzro314IFC9KlS5ckyfz589O5c+ct/h5bU9eLpzR2CduFeVcd19glAAAAFNrW+v17u1y5s3DhwiRJp06dcu6552bSpEl58sknM3369Fx//fXZc889kyQ/+clPMmzYsFrnuuSSSyrBzsEHH5yJEyfmySefzMSJE3PwwQcnScaNG5dvf/vbm5zj7bffzqBBgyrBzogRI/LQQw/l97//fa644oq0bds2b7zxRk4++eQ888wzH/TjAwAAANuQ7XLlzqBBg3L66afnpJNOyg477LBB/5IlS9K3b988//zzSZJHH300RxxxxAbjqqqq0qNHj9TU1KRnz5559NFH07p160p/dXV1+vXrlxkzZqR58+aZPXt29ttvvw3mueyyy3L55ZcnSa655ppccMEF6/VPnz49Rx55ZGpqatK/f/88/PDDH+jzv5eVO9SHlTsAAAAfjJU7W9DkyZNzyimnbDTYSZL27dvnuuuuq3w/adKkjY4bPXp0ampqkiRjx45dL9hJkh133DFjx45NktTU1GTMmDEbzLFq1arccMMNSZIePXpk5MiRG4zp06dPhg8fniSZOnVqnn766To+IQAAALC9aPBw59Of/nTuueeerFq1qqHferMcddRRlfacOXM26C+Xy/nFL36RJOnevXsOPfTQjc5z6KGH5sADD0yS3HfffXnvQqlHHnkkr7/+epJk6NChadZs4/9J1t0edu+999b3YwAAAADbuAYPdx544IGceuqp2WOPPXLeeeflz3/+c0OXUC8rV66stDcWuLz44ouVs3v69etX61xr+xcsWJB58+at17furVy1zdOzZ8+0adMmSfL444/XXjwAAACw3WjwcKdDhw4pl8v53//934wdOzb/+q//mkMOOSQ/+MEPKitYmoJp06ZV2t27d9+gf9asWbX2r2vd/nWf25x5mjdvXjmv571zAAAAANuvBg93Fi5cmF/84hc54YQT0rx585TL5cycOTNnn312OnXqlC984Qt58MEHG7qs9axevTpXXXVV5ftTTjllgzHz58+vtOs6AGntYUnvfW7d79u0aZN27drVa55XX30177zzTq1j17VgwYJavxYtWlTvuQAAAICmpXlDv+EOO+yQz3zmM/nMZz6TV199NT/5yU8yYcKE/OUvf8mKFSty55135s4778xee+2VM844I8OGDctee+3VoDWOHj06Tz75ZJJkyJAh6dmz5wZj3nrrrUq7bdu2tc63djtVsuba843NU9ccG5unZcuWdT6TrB8uAQAAANuWRr0ta/fdd883vvGNPPPMM3nqqafyla98Je3atUu5XM7f//73XH755dl3330zYMCA3HXXXeudg7O1TJs2LRdffHGSNVvIbrzxxo2OW7FiRaXdokWLWudcN4RZvnz5Ruepa4665gEAAAC2Tw2+cmdTDjnkkBxyyCEZPXp0fv7zn+eWW27Jww8/nNWrV+fhhx/Oww8/nHbt2uXzn/98vvjFL+bggw/e4jX89a9/zZAhQ1JTU5OWLVvm7rvvTseOHTc6tlWrVpV2XaHTuluo3ntd+tp56hNc1TZPbd67Fey9Fi1alN69e9d7PgAAAKDpaNSVOxvTsmXLnHrqqXnggQfy4IMP5sMf/nCl77XXXssPfvCD9OzZMx//+Mdz3333bbH3ffHFF3PMMcfktddeyw477JCJEyfWenvVTjvtVGm/d6vVey1btqzSfu/2q7Xz1DVHXfPUpnPnzrV+7bHHHvWeCwAAAGhamly4U11dndtuuy39+/fPJz7xifzjH/9IuVxOuVzOQQcdlNatW6dcLuepp57KSSedlMGDB6+3Rer9ePnll/PJT34yL7/8ckqlUm655ZYMGTKk1mfWPUR5wYIFtY5dd+XMe8+/WTvPsmXL6rwtbO08u+++e73P2wEAAAC2bU0m3Pnd736XL33pS9ljjz1yxhlnZNq0aSmXy9l5553zla98JTNmzMhf/vKXvPLKK/nhD3+YHj16pFwuZ/LkyevdbLW5lixZkgEDBmTu3LlJkrFjx+b000+v87mDDjqo0p49e3atY9ft79Gjx/uap6amJnPmzNnoHAAAAMD2q1HDnYULF+Z73/teDjzwwBx55JH58Y9/nLfeeivlcjl9+/bNhAkT8vLLL+cHP/hB/vVf/zXJmu1II0aMyLPPPpt/+7d/S7lczh133PG+3v+NN97Ipz71qfztb39Lklx11VX56le/Wq9n99lnn3Tq1CnJmkOYa/Poo48mSfbcc8907dp1vb7DDz+80q5tnhkzZlS2ZfXt27deNQIAAADbvgYPd1auXJm77747xx57bLp27ZpLLrkkL7zwQsrlctq3b5+RI0dm1qxZeeyxx3L66adv8uDgZs2a5etf/3qS5O9///tm11FdXZ3jjjsuf/zjH5Mk3/rWt3LRRRfV+/lSqZTBgwcnWbPi5oknntjouCeeeKKyImfw4MEplUrr9R911FHZZZddkiS33npryuXyRueZMGFCpV3XljEAAABg+9Hg4c4ee+yRz33uc3nggQfy7rvvplQq5Zhjjsndd9+dBQsW5Nprr82BBx5Yr7n+6Z/+KcmaLUubY+XKlRkyZEh+97vfJUnOPffcfPe73928D5LkvPPOS/Pmay4cO/vssze4nnz58uU5++yzkyTNmzfPeeedt8EcLVq0yDnnnJMkmTVrVkaNGrXBmOnTp2f8+PFJkn79+qVXr16bXSsAAACwbWrwq9Bfe+21JGsOFj7jjDPyxS9+MXvttdf7mmu33XbLd77znc1+bm24lCRHH310hg8fnr/85S+bHN+iRYt069Ztg9e7deuW888/P1dddVVmzJiRvn375qKLLsp+++2XOXPm5Oqrr87MmTOTJBdccEEOOOCAjc5/wQUX5K677srzzz+fCy+8MFVVVTn11FPTunXrTJ06NVdeeWVqamrSunXrjBkzZrM/LwAAALDtKpU3tQ9oKznppJPypS99KZ/+9Kc32KLUUDb3fffee+/Mmzdvo32rV6/OiBEjcsstt2zy+eHDh2fcuHFp1mzTC6WqqqoycODAvPDCCxvt33nnnXP77bdn0KBBm1V7fSxYsKByi9f8+fPXuwmsCLpePKWxS9guzLvquMYuAQAAoNC21u/fDb5y52c/+1lDv+VW1axZs4wfPz4nnXRSxo0bl6eeeipLlixJ+/bt06tXr3z5y1/OscceW+c8+++/f2bOnJnvf//7ueeee1JVVZWVK1emS5cuGThwYM4999zsvffeDfCJAAAAgCJp8JU7ND1W7lAfVu4AAAB8MNvMyp233noro0ePTpKceeaZ+fCHP1zr+EWLFuVHP/pRkjVn02zq9iwAAACA7VGD35Z133335bLLLsvtt99eZ7CTJB/+8Idz++235/LLL88vf/nLBqgQAAAAoDgaPNy59957UyqVcsopp9RrfKlUyqmnnppyuZx77rlnK1cHAAAAUCwNHu7Mnj07SXLYYYfV+5k+ffokSf72t79tlZoAAAAAiqrBw50FCxYkSfbYY496P7N2+9bChQu3Sk0AAAAARdXg4U6zZmvesrq6ut7PrB1bU1OzVWoCAAAAKKoGD3fWrtiZMWNGvZ9ZO7Y+BzADAAAAbE8aPNw54ogjUi6X84Mf/CCrVq2qc/yqVavygx/8IKVSKYcffngDVAgAAABQHA0e7pxxxhlJkhdeeCGf//zna92eVV1dnc997nN5/vnn13sWAAAAgDWaN/QbHnbYYTn11FNz55135t57780f/vCHjBgxIkceeWT22GOPlEqlvPzyy3n00Udz8803Z8GCBSmVSvnsZz+bfv36NXS5AAAAAE1ag4c7SXLLLbdkyZIlefDBB7Nw4cJcdtllGx1XLpeTJAMGDMitt97agBUCAAAAFEODb8tKklatWuU3v/lNRo8enU6dOqVcLm/0q0uXLvmf//mf3H///WnVqlVjlAoAAADQpDXKyp0kKZVKOffcc3POOefkT3/6U2bOnJklS5YkSdq3b59//dd/zf/7f/8vpVKpsUoEAAAAaPIaLdxZq1Qq5eCDD87BBx/c2KUAAAAAFE6jbMsCAAAAYMsQ7gAAAAAUWKNuy/rzn/+cxx57LHPnzs1bb72Vd999t9bxpVIp48ePb6DqAAAAAJq+Rgl3nnvuuXzxi1/ME088Ue9nyuWycAcAAADgPRo83Fm4cGGOPPLILFmyJOVyOUnStm3b7LrrrmnWzC4xAAAAgM3R4OHOFVdckVdffTWlUilf+tKXcv7556dbt24NXQYAAADANqHBw537778/pVIpp59+esaNG9fQbw8AAACwTWnwfVAvv/xykuT0009v6LcGAAAA2OY0eLiz6667JknatWvX0G8NAAAAsM1p8HCnZ8+eSZLnn3++od8aAAAAYJvT4OHOOeeck3K57LwdAAAAgC2gwcOdAQMG5MILL8zUqVNz1llnZdWqVQ1dAgAAAMA2o8Fvy7rtttty0EEH5bDDDsu4cePyy1/+Mp/97GfTvXv37LjjjnU+7yBmAAAAgP/T4OHOsGHDUiqVKt8vWrQoY8eOrdeza69QBwAAAGCNBg93kqRcLjfG2wIAAABscxo83HnxxRcb+i0BAAAAtlkNHu7svffeDf2WAAAAANusBr8tCwAAAIAtR7gDAAAAUGCNcqDyWlVVVbntttsyffr0vPLKK1m+fHnuv//+7L///pUxf/nLX/LSSy+lTZs26devXyNWCwAAAND0NEq4s3r16lx00UUZM2ZMVq9eXbk9q1QqZeXKleuNnT9/fgYNGpTmzZvnxRdfzJ577tkYJQMAAAA0SY2yLevLX/5yrr/++rz77rvp1KlTPvvZz25y7LHHHpt999037777biZNmtSAVQIAAAA0fQ0e7jzyyCMZP358kuSb3/xm5s2bl7vvvrvWZ04++eSUy+VMnTq1IUoEAAAAKIwG35Z10003JUkGDhyY7373u/V6pnfv3kmSv/71r1utLgAAAIAiavCVO9OnT0+pVMrw4cPr/Uznzp2TJK+88srWKgsAAACgkBo83Fm8eHGSZJ999qn3M82br1lgtGrVqq1SEwAAAEBRNXi407p16yRJdXV1vZ956aWXkiS77rrrVqkJAAAAoKgaPNxZu2Jn5syZ9X5m8uTJSZKDDjpoq9QEAAAAUFQNHu4cc8wxKZfLGTduXFavXl3n+Keffjo/+clPUiqV8ulPf7oBKgQAAAAojgYPd772ta+ldevWefbZZzNixIhaz9H52c9+lk9/+tNZuXJldt5555x55pkNWCkAAABA09fgV6Hvueee+Z//+Z+MGDEiEyZMyAMPPJDPfOYzlf7x48enuro6Dz74YObOnZtyuZxSqZRx48Zll112aehyAQAAAJq0Bg93kmT48OEplUo555xzsnDhwvzwhz9MqVRKkowZMyZJUi6XkyQtW7bMTTfdlJNPPrkxSgUAAABo0hp8W9ZaX/ziFzN79ux84xvfyH777Zdyubze15577pmzzjors2bNytChQxurTAAAAIAmrVFW7qzVuXPnjBo1KqNGjcqbb76ZxYsX5913380//dM/pX379o1ZGgAAAEAhNGq4s66dd945O++8c2OXAQAAAFAojbYtCwAAAIAPTrgDAAAAUGANvi3r6KOPft/PlkqlPPTQQ1uwGgAAAIBia/Bw55FHHkmpVKpcdb4xa69FX2vt2Pe+DgAAALC9a/Bw58gjj6wzpFm2bFleeOGFvPHGGymVSunWrVv22GOPBqoQAAAAoDgaZeVOfZTL5UyZMiXnnntu/vd//zc333xzDj/88K1bHAAAAEDBNNkDlUulUgYNGpTHH388O+ywQ4YMGZKFCxc2dlkAAAAATUqTDXfW2mOPPfKNb3wjS5cuzTXXXNPY5QAAAAA0KU0+3ElS2Y41ZcqURq4EAAAAoGkpRLjTokWLJMnLL7/cyJUAAAAANC2FCHcef/zxJMmOO+7YyJUAAAAANC1NPtyZPn16/uu//iulUim9e/du7HIAAAAAmpQGvwr9v/7rv+ocs3r16rz22muZMWNG/vCHP2T16tUplUr5+te/3gAVAgAAABRHg4c7l112WUqlUr3Hl8vlNG/ePNdcc00GDBiwFSsDAAAAKJ4GD3eSNYFNbUqlUnbaaafss88+6devX84888wcdNBBDVQdAAAAQHE0eLizevXqhn5LAAAAgG1Wkz9QGQAAAIBNE+4AAAAAFJhwBwAAAKDAGvzMnZdeemmrzLvXXnttlXkBAAAAmrIGD3f22WefLT5nqVRKTU3NFp8XAAAAoKlr8HCnrmvQAQAAAKi/Bg93fvzjHydJfvCDH+Spp57Khz70oRxzzDHp3bt3OnbsmHK5nMWLF+epp57KAw88kFWrVqVXr14566yzGrpUAAAAgCavwcOdoUOH5ktf+lJmzJiRY445JuPHj8+ee+650bELFy7MiBEj8pvf/CYf/ehH86Mf/aiBqwUAAABo2hr8tqxJkybllltuSc+ePTNlypRNBjtJsueee+aXv/xlDjnkkNxyyy25++67G7BSAAAAgKavwcOdH/7whymVSvnGN76RHXbYoc7xO+ywQ0aOHJlyuZxx48Y1QIUAAAAAxdHg4c4zzzyTJOnWrVu9n1k79tlnn90qNQEAAAAUVYOHO2+99VaSZPHixfV+Zu3Ytc8CAAAAsEaDhzt77713kuS2226r9zNrx+61115bpSYAAACAomrwcGfw4MEpl8u58847c80119Q5ftSoUZk4cWJKpVKGDBnSABUCAAAAFEeDX4V+8cUX57bbbss//vGP/Od//mcmTpyYoUOHplevXunQoUNKpVL+8Y9/5KmnnspPfvKT/OlPf0qSfPjDH85FF13U0OUCAAAANGkNHu60a9cuDz74YD71qU9l4cKFeeaZZzJy5MhNji+Xy+ncuXPuv//+tGvXruEKBQAAACiABt+WlSQHHXRQ/vrXv+brX/962rVrl3K5vNGvdu3a5Rvf+Eb+8pe/5KCDDmqMUgEAAACatAZfubPWzjvvnOuuuy7f+9738vTTT+fZZ5/Na6+9lnK5nN122y0f/ehHc8ghh6RFixaNVSIAAABAk9do4c5aLVq0SJ8+fdKnT5/GLgUAAACgcBplWxYAAAAAW0ajr9yZO3dupk+fnldeeSXV1dU566yz0r59+8YuCwAAAKAQGm3lzsyZM9OvX78ccMABOf3003PhhRfmsssuy+LFi9cb9/3vfz8dOnTIAQcckFWrVm2x91+8eHEmT56cSy+9NMcee2zat2+fUqmUUqmUYcOG1WuOCRMmVJ6p62vChAl1zlddXZ1rr702vXv3zm677Za2bdumR48eOf/88/PSSy99sA8MAAAAbJMaZeXOlClT8tnPfjYrV65MuVyuvF4qlTYYO3To0Fx88cVZunRpJk+enCFDhmyRGjp27LhF5tlS5syZk+OOOy7PPffceq/Pnj07s2fPzs0335w77rgjAwcObKQKAQAAgKaowVfuvPLKK/nc5z6Xd955JwcddFB+/etf56233trk+LZt2+aEE05Ikvz617/eKjV16dIlxxxzzAea4ze/+U2effbZTX6t/Qwb8/bbb2fQoEGVYGfEiBF56KGH8vvf/z5XXHFF2rZtmzfeeCMnn3xynnnmmQ9UJwAAALBtafCVO6NHj87bb7+dvffeO4899ljatWtX5zNHHXVUbr/99jz99NNbrI5LL700vXr1Sq9evdKxY8fMmzcv++yzz/uer1u3bunatev7enbUqFGZPXt2kuSaa67JBRdcUOnr06dP+vfvnyOPPDLV1dU577zz8vDDD7/vOgEAAIBtS4Ov3PnNb36TUqmUkSNH1ivYSZIDDzwwSTJv3rwtVsfll1+eQYMGNfr2rFWrVuWGG25IkvTo0SMjR47cYEyfPn0yfPjwJMnUqVO3aMgFAAAAFFuDhzsvvvhikqR37971fmannXZKsmb70rbmkUceyeuvv55kzflCzZpt/D/Juoc833vvvQ1QGQAAAFAEDR7urL3x6kMf+lC9n1kbfrRp02ZrlNSoHnvssUq7X79+mxzXs2fPyud//PHHt3pdAAAAQDE0eLjz4Q9/OMn/reCpj+nTpydJOnfuvFVq2hKGDRuWjh07pkWLFmnfvn0OPfTQXHLJJVm4cGGtz82aNavS7t69+ybHNW/ePPvtt98GzwAAAADbtwYPd/r27Zsk+fnPf16v8dXV1bnppptSKpVy5JFHbs3SPpBp06Zl8eLFWbVqVZYuXZo//OEPueKKK7L//vvnhz/84Safmz9/fpI1q5LqOoOoS5cuSZJXX30177zzTr1rW7BgQa1fixYtqvdcAAAAQNPS4LdlDR06NLfffnsmTpyY0047rdYryN9+++2ceuqpeemll1IqlSqHCjcl++67b0488cT06dOnEr7MnTs3P/vZzzJp0qSsWLEiX/nKV1IqlXLmmWdu8Pzaa+Dbtm1b53utuy3t7bffTsuWLetV49q6AAAAgG1Pg4c7n/zkJ3PCCSfkvvvuy/HHH5+zzz47J598cqX/f//3f/OHP/whDzzwQG666aa88sorKZVKOf3003PwwQc3dLm1GjJkSIYOHZpSqbTe67169cq//du/ZfLkyTnxxBOzatWqfP3rX8/xxx9f2Za21ooVK5IkLVq0qPP91g1zli9fvgU+AQAAAFB0DR7uJMlPf/rTDBo0KI888kiuv/76XH/99ZWAZN1DhcvlcpLkE5/4RG666abGKLVWu+yyS639gwYNyne+851ccsklqa6uzvjx4/Otb31rvTGtWrVKkqxcubLO91t3K1br1q3rXefarV+bsmjRos26vQwAAABoOhr8zJ0k2XHHHfPggw/m2muvzYc//OGUy+WNfu2222658sor85vf/KbeW5CamhEjRlSCq2nTpm3QvznXvC9btqzSrs82rrU6d+5c69cee+xR77kAAACApqVRVu4kSbNmzTJy5Mice+65efLJJzNjxowsXrw47777bv7pn/4pBx98cA4//PDChjprdejQIe3bt8+rr7660ZuzOnfunD/84Q9ZtmxZXn/99VoPVV67Amf33Xcv/J8LAAAAsGU0eLhz2223JUkOPPDAfPzjH0/z5s1z2GGH5bDDDmvoUhrM2u1lG3PQQQflZz/7WZJk9uzZOfTQQzc6rqamJnPmzEmS9OjRY8sXCQAAABRSg2/LGjZsWM4444z8/e9/b+i3bhSLFy/O0qVLkySdOnXaoP/www+vtDe2bWutGTNmVLZlrb1OHgAAAKDBw521hxAfcMABDf3WjWLcuHGVlTvrHha91lFHHVX5M7n11ls3ucpnwoQJlfaQIUO2fKEAAABAITV4uLPPPvskSV577bWGfustat68eZk5c2atYyZPnpz//u//TrLmVqwzzjhjgzEtWrTIOeeckySZNWtWRo0atcGY6dOnZ/z48UnWBES9evX6oOUDAAAA24gGP3NnyJAh+dOf/pRf/vKXOfrooxv67Ssef/zxVFVVVb5fsmRJpV1VVbXeSplkzXaydc2bNy/9+/dPnz598pnPfCYf+9jH0qFDh5TL5cydOzeTJk3KpEmTKitxRo0alT333HOjtVxwwQW566678vzzz+fCCy9MVVVVTj311LRu3TpTp07NlVdemZqamrRu3TpjxozZIp8fAAAA2DaUyrWd9rsVvPnmm/l//+//ZdGiRfnVr37VaAHPsGHDcuutt9Z7/Hv/mB555JH079+/zud23HHHjB49OmeeeWat46qqqjJw4MC88MILG+3feeedc/vtt2fQoEH1rrm+FixYkC5duiRZcyNX586dt/h7bE1dL57S2CVsF+ZddVxjlwAAAFBoW+v37wZfubPzzjvnt7/9bT772c/mU5/6VM4444x8/vOfz7/8y79k1113TalUauiS3pdDDjkkP/3pTzN9+vTMmDEjixYtypIlS1JTU5Ndd901//zP/5xPfOIT+dKXvpQOHTrUOd/++++fmTNn5vvf/37uueeeVFVVZeXKlenSpUsGDhyYc889N3vvvXcDfDIAAACgSBp85c4OO+xQaZfL5c0Kc0qlUmpqarZGWds1K3eoDyt3AAAAPphtZuXOe7OkBs6WAAAAALYpDR7ufOc732notwQAAADYZm3VcOe2225LkpxwwgnZeeedkwh3AAAAALakrRruDBs2LKVSKT179sxBBx20Qf+rr76aG2+8MaVSKd/+9re3ZikAAAAA26QG35a1rsWLF+eyyy4T7gAAAAC8T80auwAAAAAA3j/hDgAAAECBCXcAAAAACky4AwAAAFBgwh0AAACAAhPuAAAAABRYg1yF/oMf/CAdOnTY4PXFixdX2v/1X/9Vr7kuvfTSLVYXAAAAQNE1SLhz4403brKvVColSS6//PJ6zSXcAQAAAPg/Wz3cKZfLW2yutUEQAAAAAGts1XBn6tSpW3N6AAAAgO3eVg13+vXrtzWnBwAAANjuuS0LAAAAoMCEOwAAAAAFJtwBAAAAKDDhDgAAAECBCXcAAAAACky4AwAAAFBgwh0AAACAAhPuAAAAABSYcAcAAACgwIQ7AAAAAAUm3AEAAAAoMOEOAAAAQIEJdwAAAAAKTLgDAAAAUGDCHQAAAIACE+4AAAAAFJhwBwAAAKDAhDsAAAAABSbcAQAAACgw4Q4AAABAgQl3AAAAAApMuAMAAABQYMIdAAAAgAIT7gAAAAAUmHAHAAAAoMCEOwAAAAAFJtwBAAAAKDDhDgAAAECBCXcAAAAACky4AwAAAFBgwh0AAACAAhPuAAAAABSYcAcAAACgwIQ7AAAAAAUm3AEAAAAoMOEOAAAAQIEJdwAAAAAKTLgDAAAAUGDCHQAAAIACE+4AAAAAFJhwBwAAAKDAhDsAAAAABSbcAQAAACgw4Q4AAABAgQl3AAAAAApMuAMAAABQYMIdAAAAgAIT7gAAAAAUmHAHAAAAoMCEOwAAAAAFJtwBAAAAKDDhDgAAAECBCXcAAAAACky4AwAAAFBgwh0AAACAAhPuAAAAABSYcAcAAACgwIQ7AAAAAAUm3AEAAAAoMOEOAAAAQIEJdwAAAAAKTLgDAAAAUGDCHQAAAIACE+4AAAAAFJhwBwAAAKDAhDsAAAAABSbcAQAAACgw4Q4AAABAgQl3AAAAAApMuAMAAABQYNttuLN48eJMnjw5l156aY499ti0b98+pVIppVIpw4YN2+z57r///px44onp3LlzWrZsmc6dO+fEE0/M/fffX+85qqurc+2116Z3797Zbbfd0rZt2/To0SPnn39+Xnrppc2uCQAAANj2NW/sAhpLx44dt8g85XI5X/nKVzJu3Lj1Xl+4cGF+/vOf5+c//3nOPPPM3HTTTSmVSpucZ86cOTnuuOPy3HPPrff67NmzM3v27Nx888254447MnDgwC1SNwAAALBt2G5X7qyrS5cuOeaYY97Xs5dcckkl2Dn44IMzceLEPPnkk5k4cWIOPvjgJMm4cePy7W9/e5NzvP322xk0aFAl2BkxYkQeeuih/P73v88VV1yRtm3b5o033sjJJ5+cZ5555n3VCQAAAGybttuVO5deeml69eqVXr16pWPHjpk3b1722WefzZqjqqoq11xzTZKkZ8+eefTRR9O6deskSa9evXL88cenX79+mTFjRq6++uqcccYZ2W+//TaYZ9SoUZk9e3aS5JprrskFF1xQ6evTp0/69++fI488MtXV1TnvvPPy8MMPv9+PDQAAAGxjttuVO5dffnkGDRr0gbZnjR49OjU1NUmSsWPHVoKdtXbccceMHTs2SVJTU5MxY8ZsMMeqVatyww03JEl69OiRkSNHbjCmT58+GT58eJJk6tSpefrpp993zQAAAMC2ZbsNdz6ocrmcX/ziF0mS7t2759BDD93ouEMPPTQHHnhgkuS+++5LuVxer/+RRx7J66+/niQZOnRomjXb+H+SdQ95vvfeez9g9QAAAMC2QrjzPr344otZuHBhkqRfv361jl3bv2DBgsybN2+9vscee2yDcRvTs2fPtGnTJkny+OOPv5+SAQAAgG2QcOd9mjVrVqXdvXv3Wseu27/uc5szT/PmzSvn9bx3DgAAAGD7td0eqPxBzZ8/v9Lu3LlzrWO7dOmy0efW/b5NmzZp165dnfM888wzefXVV/POO++kZcuW9ap1wYIFtfYvWrSoXvMAAAAATY9w53166623Ku22bdvWOnbtdqpkzbXnG5unrjk2Nk99w511wyUAAABg22Jb1vu0YsWKSrtFixa1jl03hFm+fPlG56lrjrrmAQAAALZPVu68T61ataq0V65cWevYd955p9J+73Xpa+epa4665qnNe7eCvdeiRYvSu3fves8HAAAANB3Cnfdpp512qrTfu9XqvZYtW1Zpv3f71dp56pqjrnlqU9eZQAAAAEBx2Zb1Pq0bmNR1YPG6K2fee/7N2nmWLVuW119/vV7z7L777vU+bwcAAADYtgl33qeDDjqo0p49e3atY9ft79Gjx/uap6amJnPmzNnoHAAAAMD2S7jzPu2zzz7p1KlTkmTatGm1jn300UeTJHvuuWe6du26Xt/hhx9eadc2z4wZMyrbsvr27ft+SgYAAAC2QcKd96lUKmXw4MFJ1qy4eeKJJzY67oknnqisyBk8eHBKpdJ6/UcddVR22WWXJMmtt96acrm80XkmTJhQaQ8ZMuSDlg8AAABsI4Q7H8B5552X5s3XnEl99tlnb3A9+fLly3P22WcnSZo3b57zzjtvgzlatGiRc845J0kya9asjBo1aoMx06dPz/jx45Mk/fr1S69evbbkxwAAAAAKbLu9Levxxx9PVVVV5fslS5ZU2lVVVeutlEmSYcOGbTBHt27dcv755+eqq67KjBkz0rdv31x00UXZb7/9MmfOnFx99dWZOXNmkuSCCy7IAQccsNFaLrjggtx11115/vnnc+GFF6aqqiqnnnpqWrdunalTp+bKK69MTU1NWrdunTFjxnzgzw4AAABsO0rlTe0D2sYNGzYst956a73Hb+qPafXq1RkxYkRuueWWTT47fPjwjBs3Ls2abXqhVFVVVQYOHJgXXnhho/0777xzbr/99gwaNKjeNdfXggULKrd4zZ8/v3BXp3e9eEpjl7BdmHfVcY1dAgAAQKFtrd+/bcv6gJo1a5bx48dnypQpGTx4cDp16pQWLVqkU6dOGTx4cH71q1/l5ptvrjXYSZL9998/M2fOzNVXX52ePXumXbt22XHHHXPggQfm61//ep555pmtEuwAAAAAxbbdrtzh/1i5Q31YuQMAAPDBWLkDAAAAwAaEOwAAAAAFJtwBAAAAKDDhDgAAAECBCXcAAAAACky4AwAAAFBgwh0AAACAAhPuAAAAABSYcAcAAACgwIQ7AAAAAAUm3AEAAAAoMOEOAAAAQIEJdwAAAAAKTLgDAAAAUGDCHQAAAIACE+4AAAAAFJhwBwAAAKDAhDsAAAAABSbcAQAAACgw4Q4AAABAgQl3AAAAAApMuAMAAABQYMIdAAAAgAIT7gAAAAAUmHAHAAAAoMCEOwAAAAAFJtwBAAAAKDDhDgAAAECBCXcAAAAACky4AwAAAFBgwh0AAACAAhPuAAAAABSYcAcAAACgwIQ7AAAAAAUm3AEAAAAoMOEOAAAAQIEJdwAAAAAKTLgDAAAAUGDCHQAAAIACE+4AAAAAFJhwBwAAAKDAhDsAAAAABSbcAQAAACgw4Q4AAABAgQl3AAAAAApMuAMAAABQYMIdAAAAgAIT7gAAAAAUmHAHAAAAoMCEOwAAAAAFJtwBAAAAKDDhDgAAAECBCXcAAAAACky4AwAAAFBgwh0AAACAAhPuAAAAABSYcAcAAACgwIQ7AAAAAAUm3AEAAAAoMOEOAAAAQIEJdwAAAAAKTLgDAAAAUGDCHQAAAIACa97YBQDF0PXiKY1dwnZh3lXHNXYJAABAwVi5AwAAAFBgwh0AAACAAhPuAAAAABSYcAcAAACgwIQ7AAAAAAUm3AEAAAAoMOEOAAAAQIEJdwAAAAAKTLgDAAAAUGDCHQAAAIACE+4AAAAAFJhwBwAAAKDAhDsAAAAABSbcAQAAACgw4Q4AAABAgQl3AAAAAApMuAMAAABQYMIdAAAAgAIT7gAAAAAUmHAHAAAAoMCEOwAAAAAFJtwBAAAAKDDhzgdUKpXq9XXUUUfVOdf999+fE088MZ07d07Lli3TuXPnnHjiibn//vu3/gcBAAAACkm40wSUy+V8+ctfzrHHHpuf//znWbhwYVauXJmFCxfm5z//eY499th8+ctfTrlcbuxSAQAAgCameWMXsK0466yz8h//8R+b7G/Tps0m+y655JKMGzcuSXLwwQfnwgsvzH777Zc5c+bkmmuuycyZMzNu3Ljsvvvu+e53v7vFawcAAACKS7izhXTo0CEf+chHNvu5qqqqXHPNNUmSnj175tFHH03r1q2TJL169crxxx+ffv36ZcaMGbn66qtzxhlnZL/99tuitQMAAADFZVtWIxs9enRqamqSJGPHjq0EO2vtuOOOGTt2bJKkpqYmY8aMaegSAQAAgCZMuNOIyuVyfvGLXyRJunfvnkMPPXSj4w499NAceOCBSZL77rvP2TsAAABAhXCnEb344otZuHBhkqRfv361jl3bv2DBgsybN29rlwYAAAAUhHBnC7nnnnty4IEHpnXr1tlpp51ywAEHZOjQoZk6deomn5k1a1al3b1791rnX7d/3ecAAACA7ZsDlbeQv/3tb+t9X1VVlaqqqtx222054YQTMmHChOyyyy7rjZk/f36l3blz51rn79Kly0afq48FCxbU2r9o0aLNmg8AAABoOoQ7H9COO+6Y448/Pp/4xCfSvXv3tG3bNq+++mqmTZuWm266KUuXLs19992XwYMH57e//W0+9KEPVZ596623Ku22bdvW+j7rXqX+9ttvb1aN6wZDAAAAwLZFuPMBLVy4MO3atdvg9QEDBuTss8/Osccem5kzZ2batGm58cYbc84551TGrFixotJu0aJFre/TsmXLSnv58uUfvHAAAABgmyDc+YA2Fuys1bFjx0yaNCk9evTIypUrM3bs2PXCnVatWlXaK1eurPV93nnnnUr7vdel16WubVyLFi1K7969N2tOAAAAoGkQ7mxl++67bwYMGJApU6akqqoqL7/8cjp16pQk2WmnnSrj6tpqtWzZskq7ri1c71XXeT4AAABAcbktqwEcdNBBlfbaq8+T9UOXug49Xnf1jTN0AAAAgLWEOw2gXC5v9PV1Q5/Zs2fXOse6/T169NgyhQEAAACFJ9xpAOtek752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+DlmW+DnmG2Bn2O2BdvDz3FNTU1effXVJMlHP/rRLTZvMX6L34bttNNOlXZ9tlotW7YsSf22cK1V11k+yZrDnItsjz32qNfnhKbKzzDbAj/HbAv8HLMt8HPMtmBb/jneUlux1mVbViNr1apV2rdvn6TuQ6Bee+21SrizOefoAAAAANsu4U4T0KNHjyRJVVVVradlz549e4NnAAAAgO2bcKcJOPzww5Os2XL19NNPb3LctGnTKu2+fftu9boAAACApk+40wSccMIJlfaPf/zjjY5ZvXp1brvttiRJu3bt0r9//4YoDQAAAGjihDtNQO/evXPEEUckScaPH5/p06dvMOa6667LrFmzkiTnnntuPvShDzVojQAAAEDT5LasJuKGG25I3759s3z58hxzzDH55je/mf79+2f58uW58847M27cuCRJt27dMnLkyEauFgAAAGgqhDtNxMEHH5y77ror//7v/54333wz3/zmNzcY061bt0yZMmW969MBAACA7VupXC6XG7sI/s/f//733HDDDZkyZUoWLFiQFi1aZP/998/JJ5+cr33ta9lxxx0bu0QAAACgCRHuAAAAABSYA5UBAAAACky4AwAAAFBgwh0AAACAAhPuAAAAABSYcAcAAACgwIQ7AAAAAAUm3AEAAAAoMOEOAAAAQIEJdwAAAAAKTLhDIb300ks5//zz06NHj7Rp0ya77bZbevfunVGjRqW6urqxy4NNWrx4cSZPnpxLL700xx57bNq3b59SqZRSqZRhw4Y1dnlQpz/+8Y+58sorc+yxx6ZLly5p2bJl2rZtm27dumXYsGF57LHHGrtEqNWbb76ZO++8MyNHjky/fv2y//77Z5dddkmLFi3SoUOHHHXUUbnmmmuydOnSxi4V3rcLL7yw8u+LUqmURx55pLFLgo1a9+e0tq+jjjqqsUtt8krlcrnc2EXA5pgyZUq+8IUv5I033tho/4EHHphf/epX2XfffRu4MqhbqVTaZN/QoUMzYcKEhisGNlO/fv3y6KOP1jnutNNOy80335wWLVo0QFWweR588MEMGDCgznHt27fPT3/603zqU59qgKpgy/nzn/+cnj17pqampvLa1KlT/XJMk1Tbv43X1a9fPyFlHZo3dgGwOf785z/nlFNOSXV1ddq2bZv//M//TP/+/bN8+fLceeed+dGPfpTnnnsuxx13XJ566qm0bdu2sUuGTerSpUt69OiRBx54oLFLgXpZuHBhkqRTp045+eSTc8QRR2SvvfbKu+++m+nTp+e6667LwoUL85Of/CQ1NTW54447Grli2LguXbqkf//+OeSQQ9KlS5fsscceWb16dRYsWJBJkybl3nvvzZIlS3L88cfnqaeeyr/8y780dslQL6tXr86IESNSU1OTDh06ZPHixY1dEtTLWWedlf/4j//YZH+bNm0asJpiEu5QKOedd16qq6vTvHnzPPDAA+nTp0+l7+ijj84BBxyQCy+8MLNnz87111+fSy+9tBGrhQ1deuml6dWrV3r16pWOHTtm3rx52WeffRq7LKiX7t2758orr8xJJ52UHXbYYb2+Qw89NKeddlr69u2b559/PhMnTsxZZ52VI444opGqhY3r379/XnrppU32n3LKKbnvvvsyZMiQrFy5Mpdffnl+9rOfNWCF8P79z//8T5566ql07949Q4YMyfe+973GLgnqpUOHDvnIRz7S2GUUmjN3KIynnnqqshRv+PDh6wU7a40cOTI9evRIkowZMyarVq1qyBKhTpdffnkGDRqUjh07NnYpsNkmT56cU045ZYNgZ6327dvnuuuuq3w/adKkhioN6m1TP7/rOuGEE9K9e/ckqddWRGgK5s+fn29/+9tJkhtvvNHWWNjOCHcojPvuu6/SPuOMMzY6plmzZjn99NOTJK+99pp9mQANbN0zHebMmdN4hcAHtHYLwIoVKxq5Eqif//iP/8jbb7+doUOHOl8HtkPCHQpj7Q0sbdq0ySGHHLLJcf369au0H3/88a1eFwD/Z+XKlZV2s2b+mUExzZo1K3/605+SpLKCB5qyu+++O5MnT85uu+2Wa6+9trHLARqBf3VRGLNmzUqS7L///mnefNPHRa37j7C1zwDQMKZNm1Zp+6WYIqmurs4LL7yQ66+/Pv3798+7776bJDn33HMbuTKo3euvv175Ob366quz++67N3JFsPnuueeeHHjggWndunV22mmnHHDAARk6dGimTp3a2KUVhgOVKYQVK1ZkyZIlSZLOnTvXOnbXXXdNmzZtsmzZssyfP78hygMga25pueqqqyrfn3LKKY1YDdRtwoQJm9zqnSTnn39+vvCFLzRgRbD5Lrzwwrzyyis57LDDMnz48MYuB96Xv/3tb+t9X1VVlaqqqtx222054YQTMmHChOyyyy6NVF0xCHcohLfeeqvSrs/15mvDnbfffntrlgXAOkaPHp0nn3wySTJkyJD07NmzkSuC9+djH/tYbrrppnz84x9v7FKgVo8//nhuvvnmNG/ePDfddFNKpVJjlwSbZccdd8zxxx+fT3ziE+nevXvatm2bV199NdOmTctNN92UpUuX5r777svgwYPz29/+Nh/60Icau+QmS7hDIax7mGF9Tv5v2bJlkmT58uVbrSYA/s+0adNy8cUXJ1lznemNN97YyBVB3U444YRKCLl8+fLMmTMnd999d37+85/nC1/4QsaMGZNBgwY1cpWwcStXrsyZZ56Zcrmcr3/96/noRz/a2CXBZlu4cGHatWu3wesDBgzI2WefnWOPPTYzZ87MtGnTcuONN+acc85p+CILwpk7FEKrVq0q7XUP69yUd955J0nSunXrrVYTAGv89a9/zZAhQ1JTU5OWLVvm7rvvTseOHRu7LKhTu3bt8pGPfCQf+chH0qtXr5x66qm59957c9ttt2Xu3LkZPHhwJkyY0NhlwkZdeeWVmTVrVvbaa6985zvfaexy4H3ZWLCzVseOHTNp0qTK/9wfO3ZsA1VVTMIdCmGnnXaqtOuz1WrZsmVJ6reFC4D378UXX8wxxxyT1157LTvssEMmTpy43q2FUESnnXZaTj755KxevTpf+9rX8tprrzV2SbCe2bNn53vf+16SNb/wtmnTppErgq1j3333zYABA5KsOYfn5ZdfbuSKmi7bsiiEVq1apX379lmyZEkWLFhQ69jXXnutEu506dKlIcoD2C69/PLL+eQnP5mXX345pVIpt9xyS4YMGdLYZcEWMXjw4Nx9991ZtmxZfv3rX+fzn/98Y5cEFaNHj87KlSuz7777prq6OnfeeecGY/7yl79U2g8//HBeeeWVJMlnPvMZYRCFctBBB2XKlClJ1mzj6tSpUyNX1DQJdyiMHj165LHHHktVVVVqamo2eR367Nmz13sGgC1vyZIlGTBgQObOnZtkzf85Pv300xu5Kthy1r1O+u9//3sjVgIbWnsEwdy5c/O5z32uzvH//d//XWm/+OKLwh0KpVwuN3YJhWBbFoVx+OGHJ1mz5erpp5/e5Lhp06ZV2n379t3qdQFsb95444186lOfqlxbetVVV+WrX/1qI1cFW9bChQsrbdu8ARrPutekW7WzacIdCuOEE06otH/84x9vdMzq1atz2223JVlzOFf//v0bojSA7UZ1dXWOO+64/PGPf0ySfOtb38pFF13UyFXBlnfPPfdU2m4hoqmZMGFCyuVyrV/rHrI8derUyutdu3ZtvMJhM82dOze//e1vk6w5f2fPPfds5IqaLuEOhdG7d+8cccQRSZLx48dn+vTpG4y57rrrMmvWrCTJueeemw996EMNWiPAtmzlypUZMmRIfve73yVZ8/fsd7/73UauCjbPhAkTsmLFilrHjB49Or/61a+SJF27dq2sHgZgy/nlL3+ZmpqaTfb/4x//yGc/+9msWrUqSawSroMzdyiUG264IX379s3y5ctzzDHH5Jvf/Gb69++f5cuX584778y4ceOSJN26dcvIkSMbuVrY0OOPP56qqqrK90uWLKm0q6qqNrhyd9iwYQ1UGdTtc5/7XB544IEkydFHH53hw4evd2Dne7Vo0SLdunVrqPKgXi677LKMHDkyJ510Ug4//PDst99+adu2bd566608++yzuf322ysBZosWLfKjH/1ok+f8AfD+nX322Vm1alVOOumk9OnTJ127dk3r1q2zZMmSPPLII7npppuydOnSJGuO6BDu1K5UdjoRBfPLX/4y//7v/54333xzo/3dunXLlClTsv/++zdwZVC3YcOG5dZbb633eH9F05SUSqXNGr/33ntn3rx5W6cYeJ+6du1arwOSO3funFtuuaVyBS8UzWWXXZbLL788yZptWUcddVTjFgTvUd+/j0866aTcfPPNadeu3dYvqsD8bwgK5zOf+UyeeeaZ3HDDDZkyZUoWLFiQFi1aZP/998/JJ5+cr33ta9lxxx0bu0wAoAl66KGH8uCDD2bq1KmZNWtW/vGPf2Tp0qVp1apVOnbsmI997GMZNGhQTjnlFP+eANiKbr311kybNi3Tp0/P3Llzs2TJkrz55ptp27ZtunTpksMOOyxDhw5Nnz59GrvUQrByBwAAAKDAHKgMAAAAUGDCHQAAAIACE+4AAAAAFJhwBwAAAKDAhDsAAAAABSbcAQAAACgw4Q4AAABAgQl3AAAAAApMuAMAAABQYMIdAAAAgAIT7gAAAAAUmHAHAAAAoMCEOwAAAAAFJtwBAAAAKDDhDgAAAECBCXcAAAAACky4AwAAAFBgwh0AAACAAhPuAAAAABSYcAcAAACgwIQ7AAAAAAUm3AEAAAAoMOEOAAAAQIEJdwAAAAAK7P8DengKYBiVpagAAAAASUVORK5CYII="/>

#### 문제4

- 아시아 인구 백분율 전체 평균을 구하고, 평균을 초과하면 'large', 그 외에는 'small'을 부여한 파생변수를 만들어 보세요.



```python
average = midwest_new['asian_percent'].mean()
average
```

<pre>
0.4872461834357345
</pre>

```python
import numpy as np

midwest_new['group'] = np.where(midwest_new['asian_percent'] > average, 'large', 'small')
midwest_new
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>PID</th>
      <th>county</th>
      <th>state</th>
      <th>area</th>
      <th>total</th>
      <th>popdensity</th>
      <th>popwhite</th>
      <th>popblack</th>
      <th>popamerindian</th>
      <th>asian</th>
      <th>...</th>
      <th>percpovertyknown</th>
      <th>percbelowpoverty</th>
      <th>percchildbelowpovert</th>
      <th>percadultpoverty</th>
      <th>percelderlypoverty</th>
      <th>inmetro</th>
      <th>category</th>
      <th>asian_percent</th>
      <th>size</th>
      <th>group</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>561</td>
      <td>ADAMS</td>
      <td>IL</td>
      <td>0.052</td>
      <td>66090</td>
      <td>1270.961540</td>
      <td>63917</td>
      <td>1702</td>
      <td>98</td>
      <td>249</td>
      <td>...</td>
      <td>96.274777</td>
      <td>13.151443</td>
      <td>18.011717</td>
      <td>11.009776</td>
      <td>12.443812</td>
      <td>0</td>
      <td>AAR</td>
      <td>0.376759</td>
      <td>small</td>
      <td>small</td>
    </tr>
    <tr>
      <th>1</th>
      <td>562</td>
      <td>ALEXANDER</td>
      <td>IL</td>
      <td>0.014</td>
      <td>10626</td>
      <td>759.000000</td>
      <td>7054</td>
      <td>3496</td>
      <td>19</td>
      <td>48</td>
      <td>...</td>
      <td>99.087145</td>
      <td>32.244278</td>
      <td>45.826514</td>
      <td>27.385647</td>
      <td>25.228976</td>
      <td>0</td>
      <td>LHR</td>
      <td>0.451722</td>
      <td>small</td>
      <td>small</td>
    </tr>
    <tr>
      <th>2</th>
      <td>563</td>
      <td>BOND</td>
      <td>IL</td>
      <td>0.022</td>
      <td>14991</td>
      <td>681.409091</td>
      <td>14477</td>
      <td>429</td>
      <td>35</td>
      <td>16</td>
      <td>...</td>
      <td>94.956974</td>
      <td>12.068844</td>
      <td>14.036061</td>
      <td>10.852090</td>
      <td>12.697410</td>
      <td>0</td>
      <td>AAR</td>
      <td>0.106731</td>
      <td>small</td>
      <td>small</td>
    </tr>
    <tr>
      <th>3</th>
      <td>564</td>
      <td>BOONE</td>
      <td>IL</td>
      <td>0.017</td>
      <td>30806</td>
      <td>1812.117650</td>
      <td>29344</td>
      <td>127</td>
      <td>46</td>
      <td>150</td>
      <td>...</td>
      <td>98.477569</td>
      <td>7.209019</td>
      <td>11.179536</td>
      <td>5.536013</td>
      <td>6.217047</td>
      <td>1</td>
      <td>ALU</td>
      <td>0.486918</td>
      <td>small</td>
      <td>small</td>
    </tr>
    <tr>
      <th>4</th>
      <td>565</td>
      <td>BROWN</td>
      <td>IL</td>
      <td>0.018</td>
      <td>5836</td>
      <td>324.222222</td>
      <td>5264</td>
      <td>547</td>
      <td>14</td>
      <td>5</td>
      <td>...</td>
      <td>82.505140</td>
      <td>13.520249</td>
      <td>13.022889</td>
      <td>11.143211</td>
      <td>19.200000</td>
      <td>0</td>
      <td>AAR</td>
      <td>0.085675</td>
      <td>small</td>
      <td>small</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>432</th>
      <td>3048</td>
      <td>WAUKESHA</td>
      <td>WI</td>
      <td>0.034</td>
      <td>304715</td>
      <td>8962.205880</td>
      <td>298313</td>
      <td>1096</td>
      <td>672</td>
      <td>2699</td>
      <td>...</td>
      <td>98.387674</td>
      <td>3.121060</td>
      <td>3.785820</td>
      <td>2.590061</td>
      <td>4.085479</td>
      <td>1</td>
      <td>HLU</td>
      <td>0.885746</td>
      <td>large</td>
      <td>large</td>
    </tr>
    <tr>
      <th>433</th>
      <td>3049</td>
      <td>WAUPACA</td>
      <td>WI</td>
      <td>0.045</td>
      <td>46104</td>
      <td>1024.533330</td>
      <td>45695</td>
      <td>22</td>
      <td>125</td>
      <td>92</td>
      <td>...</td>
      <td>96.330036</td>
      <td>8.488697</td>
      <td>10.071411</td>
      <td>6.953799</td>
      <td>10.338641</td>
      <td>0</td>
      <td>AAR</td>
      <td>0.199549</td>
      <td>small</td>
      <td>small</td>
    </tr>
    <tr>
      <th>434</th>
      <td>3050</td>
      <td>WAUSHARA</td>
      <td>WI</td>
      <td>0.037</td>
      <td>19385</td>
      <td>523.918919</td>
      <td>19094</td>
      <td>29</td>
      <td>70</td>
      <td>43</td>
      <td>...</td>
      <td>98.854785</td>
      <td>13.786985</td>
      <td>20.050708</td>
      <td>11.695784</td>
      <td>11.804558</td>
      <td>0</td>
      <td>AAR</td>
      <td>0.221821</td>
      <td>small</td>
      <td>small</td>
    </tr>
    <tr>
      <th>435</th>
      <td>3051</td>
      <td>WINNEBAGO</td>
      <td>WI</td>
      <td>0.035</td>
      <td>140320</td>
      <td>4009.142860</td>
      <td>136822</td>
      <td>697</td>
      <td>685</td>
      <td>1728</td>
      <td>...</td>
      <td>95.460376</td>
      <td>8.804031</td>
      <td>10.592031</td>
      <td>8.660587</td>
      <td>6.661094</td>
      <td>1</td>
      <td>HAU</td>
      <td>1.231471</td>
      <td>large</td>
      <td>large</td>
    </tr>
    <tr>
      <th>436</th>
      <td>3052</td>
      <td>WOOD</td>
      <td>WI</td>
      <td>0.048</td>
      <td>73605</td>
      <td>1533.437500</td>
      <td>72157</td>
      <td>90</td>
      <td>481</td>
      <td>722</td>
      <td>...</td>
      <td>98.750085</td>
      <td>8.525831</td>
      <td>11.162997</td>
      <td>7.375656</td>
      <td>7.882918</td>
      <td>0</td>
      <td>AAR</td>
      <td>0.980912</td>
      <td>large</td>
      <td>large</td>
    </tr>
  </tbody>
</table>
<p>437 rows × 31 columns</p>
</div>


#### 문제 5:

- 'large'와 'small'에 해당하는 지역이 얼마나 많은지 빈도표와 빈도 막대 그래프를 만들어 확인해 보세요



```python
count_group = midwest_new['group'].value_counts()
count_group
```

<pre>
group
small    318
large    119
Name: count, dtype: int64
</pre>

```python
count_group.plot.bar(rot = 0)
```

<pre>
<Axes: xlabel='group'>
</pre>
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABFAAAANhCAYAAADABk+6AAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjcuMiwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8pXeV/AAAACXBIWXMAAB7CAAAewgFu0HU+AABVxUlEQVR4nO3de5yWZYH/8e/gyFkhA0yEQlESK9MNSEJFSy2RFcE8dFJcRe1g6grWtlb2K8+26voz/bGiuKVmmodVy0pD8IApykatkIKigJTAggfOI/P7w+VZkJm5RmVgGN7v18vX657nvu7ruR7+8GE+3Ieq2tra2gAAAABQr1abewEAAAAAzZ2AAgAAAFAgoAAAAAAUCCgAAAAABQIKAAAAQIGAAgAAAFAgoAAAAAAUCCgAAAAABQIKAAAAQIGAAgAAAFAgoAAAAAAUCCgAAAAABQIKAAAAQIGAAgAAAFAgoAAAAAAUCCgAAAAABdWbewFbixUrVuRPf/pTkqRr166prvZHDwAAABtbTU1NFixYkCT52Mc+lrZt226Uef0Wv4n86U9/yoABAzb3MgAAAGCr8cQTT6R///4bZS6X8AAAAAAUOANlE+natWtl+4knnshOO+20GVcDAAAALdP8+fMrV4Cs+7v4eyWgbCLr3vNkp512So8ePTbjagAAAKDl25j3H3UJDwAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAXVm3sB0JL1+vZ9m3sJQBOZfdHhm3sJAABsQs5AAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKBBQAAACAAgEFAAAAoEBAAQAAACgQUAAAAAAKmiygvPbaa/n5z3+es88+O4MHD85uu+2WTp06pXXr1unWrVsOPPDAXHLJJVm0aFGj5rv//vszYsSI9OjRI23atEmPHj0yYsSI3H///Y1e07Jly3LppZdmwIAB2WGHHdKxY8f07ds3o0ePzksvvfRuPyoAAADQwlXV1tbWNsXEDzzwQA455JDiuC5duuRnP/tZPvvZz9a5v7a2NqeddlrGjh1b7xynnHJKrr322lRVVdU7ZtasWTn88MPzl7/8pc79nTp1ys0335whQ4YU1/xuzJ07Nz179kySzJkzJz169GiS96F56fXt+zb3EoAmMvuiwzf3EgAAqENT/f7dpJfw9OzZM8cff3yuvPLK3HHHHZk8eXIeffTR3HrrrTn66KOzzTbbZOHChTniiCMybdq0Ouc499xzK/Fkn332yS233JInnngit9xyS/bZZ58kydixY/Pd73633nW88cYbGTp0aCWejBo1Kg8++GAee+yxnH/++enYsWNeffXVHH300fWuAwAAANh6NdkZKG+++Wa22WabBsfcddddGT58eJJkxIgR+eUvf7ne/pkzZ6Zv376pqalJv379MmnSpLRr166yf9myZRk8eHCmTJmS6urqzJgxI717997gfc4777z84Ac/SJJccsklGTNmzHr7J0+enAMOOCA1NTU56KCD8vvf//5dfeaGOANl6+QMFGi5nIECANA8bXFnoJTiSZIceeSR2WOPPZIkkyZN2mD/5ZdfnpqamiTJVVddtV48SZL27dvnqquuSpLU1NTkiiuu2GCO1atX58orr0yS9O3bN2efffYGYwYOHJiTTjopSTJhwoQ89dRTxbUDAAAAW4/N/hSeDh06JElWrFix3uu1tbW5++67kyR77LFH9t133zqP33ffffPhD384yVtntLz9hJqHHnooS5YsSZKccMIJadWq7o88cuTIyvYdd9zxjj8HAAAA0HJt1oAyffr0/Od//meSVM5EWeuFF17IvHnzkiSDBw9ucJ61++fOnZvZs2evt+/hhx/eYFxd+vXrV4k5jzzySKPWDwAAAGwdqjf1Gy5btizz5s3LPffck0suuSRvvvlmkuSMM85Yb9z06dMr22+PK2+37v7p06dnl112ecfzVFdXp3fv3pk2bdp6xzTW3LlzG9w/f/78dzwnAAAA0DxskoAyfvz4nHjiifXuHz16dL70pS+t99qcOXMq26Ubvqy9Oczbj1v35w4dOqRz587FeaZNm5YFCxZk5cqVadOmTYPj61sDAAAA0LJs8jNQ1rX33nvn2muvzSc/+ckN9r3++uuV7Y4dOzY4z9pLb5K3Hllc1zylOeqa550EFAAAAKDl2iQB5cgjj0y/fv2SJMuXL8+sWbPyi1/8InfeeWe+9KUv5YorrsjQoUPXO2bdm8q2bt26wfnXDR3Lly+vc57SHKV5St5+5svbzZ8/PwMGDHhHcwIAAADNwyYJKJ07d17v8pn+/fvnuOOOy09/+tOccMIJGTZsWMaNG7fek3Datm1b2V61alWD869cubKy/fZHHa+dpzRHaZ6SjfVcaQAAAKD52axP4fnKV76So48+OmvWrMk3vvGNLF68uLJvu+22q2y//bKct1u6dGll++2X6qydpzRHaR4AAABg67VZA0qSDBs2LMlb8eLXv/515fV1z+goPeFm3ctn3n4z17XzLF26NEuWLGnUPF27dnX/EwAAAKBisweUrl27VrZffPHFyvaee+5Z2Z4xY0aDc6y7v2/fvuvta+w8NTU1mTVrVp1zAAAAAFu3zR5Q5s2bV9le97KZXXbZJd27d0+STJw4scE5Jk2alCTZeeed06tXr/X27bfffpXthuaZMmVK5RKeQYMGNW7xAAAAwFZhsweU2267rbL9sY99rLJdVVVVubxnxowZefzxx+s8/vHHH6+cWTJs2LBUVVWtt//AAw9Mp06dkiQ33nhjamtr65xn/Pjxle3hw4e/8w8CAAAAtFhNFlDGjx+/3qOI63L55ZfnV7/6VZKkV69e650tkiRnnnlmqqvfelDQ6aefvsGjhZcvX57TTz89SVJdXZ0zzzxzg/do3bp1vvnNbyZJpk+fnssuu2yDMZMnT864ceOSJIMHD07//v0b8QkBAACArUWTPcb4vPPOy9lnn52jjjoq++23X3r37p2OHTvm9ddfz5/+9KfcdNNNefTRR5O8FTn+7d/+rRJL1urTp09Gjx6diy66KFOmTMmgQYPyrW99K717986sWbNy8cUXZ+rUqUmSMWPGZPfdd69zLWPGjMmtt96aZ599Nuecc05mzpyZ4447Lu3atcuECRNywQUXpKamJu3atcsVV1zRVH8kAAAAwBaqqra+a1reo169eq13U9j69OjRI9dff30OOeSQOvevWbMmo0aNyvXXX1/vHCeddFLGjh2bVq3qP6Fm5syZGTJkSJ577rk692+//fa56aabMnTo0OKa3425c+dWnhA0Z86c9Z4yRMvV69v3be4lAE1k9kWHb+4lAABQh6b6/bvJzkB58MEH88ADD2TChAmZPn16/va3v2XRokVp27Ztdtxxx+y9994ZOnRojjnmmLRv377eeVq1apVx48blqKOOytixY/Pkk09m4cKF6dKlS/r3759TTz01hx12WHE9u+22W6ZOnZqrr746t912W2bOnJlVq1alZ8+eGTJkSM4444x86EMf2ph/BAAAAEAL0WRnoLA+Z6BsnZyBAi2XM1AAAJqnpvr9e7M/hQcAAACguRNQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKGjSgPL000/nggsuyGGHHZaePXumTZs26dixY/r06ZORI0fm4YcfLs4xfvz4VFVVNeq/8ePHF+dbtmxZLr300gwYMCA77LBDOnbsmL59+2b06NF56aWXNsKnBgAAAFqa6qaaePDgwZk0adIGr69atSrPPfdcnnvuudx44435yle+kuuuuy6tW7duqqVUzJo1K4cffnj+8pe/rPf6jBkzMmPGjFx33XW5+eabM2TIkCZfCwAAALDlaLKAMm/evCRJ9+7dc/TRR2f//ffPBz/4wbz55puZPHlyfvzjH2fevHn56U9/mpqamtx8883FOX/zm9+ke/fu9e7v0aNHvfveeOONDB06tBJPRo0aleOOOy7t2rXLhAkTcuGFF+bVV1/N0UcfncmTJ2evvfZ6h58YAAAAaKmaLKDsscceueCCC3LUUUdlm222WW/fvvvum6985SsZNGhQnn322dxyyy356le/mv3337/BOfv06ZNevXq9q/VcdtllmTFjRpLkkksuyZgxYyr7Bg4cmIMOOigHHHBAli1bljPPPDO///3v39X7AAAAAC1Pk90D5d57780xxxyzQTxZq0uXLvnxj39c+fn2229vqqVk9erVufLKK5Mkffv2zdlnn73BmIEDB+akk05KkkyYMCFPPfVUk60HAAAA2LJs1qfwHHjggZXtWbNmNdn7PPTQQ1myZEmS5IQTTkirVnV/7JEjR1a277jjjiZbDwAAALBl2awBZdWqVZXt+qLGxrDu034GDx5c77h+/fqlQ4cOSZJHHnmkydYDAAAAbFma7B4ojTFx4sTK9h577FEcP3LkyEyfPj2LFy/O9ttvn9122y0HH3xwvvrVr2bnnXeu97jp06c36n2qq6vTu3fvTJs2bb1jGmPu3LkN7p8/f/47mg8AAABoPjZbQFmzZk0uuuiiys/HHHNM8Zh1g8uiRYuyaNGi/OEPf8iPf/zjXHHFFTn11FPrPG7OnDlJkg4dOqRz584NvkfPnj0zbdq0LFiwICtXrkybNm0a8WneOg4AAABomTZbQLn88svzxBNPJEmGDx+efv361Tt21113zYgRIzJw4MBKqHj++efzy1/+MrfffntWrFiR0047LVVVVTnllFM2OP71119PknTs2LG4rrWX8CRvPfq4sQEFAAAAaLk2S0CZOHFivv3tbydJunXrlmuuuabescOHD88JJ5yQqqqq9V7v379/jj322Nx7770ZMWJEVq9enbPOOitHHHFEPvCBD6w3dsWKFUmS1q1bF9e2bjBZvnx5oz/T2rNc6jN//vwMGDCg0fMBAAAAzccmv4nsf/3Xf2X48OGpqalJmzZt8otf/CI77rhjveM7deq0QTxZ19ChQ/P9738/SbJs2bKMGzdugzFt27ZNsv5Na+uzcuXKyna7du2K49fq0aNHg//ttNNOjZ4LAAAAaF42aUB54YUXcuihh2bx4sXZZpttcssttzT4VJzGGjVqVCWyrHuflLW22267JG9dklOydOnSynZjLvkBAAAAWr5NFlBefvnlHHzwwXn55ZdTVVWV66+/PsOHD98oc3fr1i1dunRJksybN2+D/T169EjyVhxZsmRJg3OtvRSna9eu7n8CAAAAJNlEAWXhwoU55JBD8vzzzydJrrrqqhx//PEb9T1qa2vr3bfnnntWtmfMmFHvuJqamsyaNStJ0rdv3423OAAAAGCL1uQB5dVXX81nP/vZPPPMM0mSiy66KF//+tc36nu88sorWbRoUZKke/fuG+zfb7/9Ktt1XeKz1pQpUyqX8AwaNGijrhEAAADYcjVpQFm2bFkOP/zwPP3000mSf/7nf863vvWtjf4+Y8eOrZyBUtc9VQ488MB06tQpSXLjjTfWe7bK+PHjK9sb6/IiAAAAYMvXZAFl1apVGT58eB599NEkyRlnnJEf/ehH72iO2bNnZ+rUqQ2Ouffee/PDH/4wyVtP2znxxBM3GNO6det885vfTJJMnz49l1122QZjJk+eXHmCz+DBg9O/f/93tFYAAACg5apuqom/8IUv5Le//W2S5NOf/nROOumk/PnPf653fOvWrdOnT5/1Xps9e3YOOuigDBw4MH//93+fvffeO926dUttbW2ef/753H777bn99tsrZ5Rcdtll2Xnnneucf8yYMbn11lvz7LPP5pxzzsnMmTNz3HHHpV27dpkwYUIuuOCC1NTUpF27drniiis2zh8CAAAA0CJU1TZ099X3MvH/PFa4sT70oQ9l9uzZ67320EMP5aCDDioe2759+1x++eU55ZRTGhw3c+bMDBkyJM8991yd+7fffvvcdNNNGTp0aKPX3Vhz585Nz549k7z1pJ+1TwaiZev17fs29xKAJjL7osM39xIAAKhDU/3+3WRnoGwMn/jEJ/Kzn/0skydPzpQpUzJ//vwsXLgwNTU1ed/73pePfOQj+cxnPpOTTz453bp1K8632267ZerUqbn66qtz2223ZebMmVm1alV69uyZIUOG5IwzzsiHPvShTfDJAAAAgC1Jk52BwvqcgbJ1cgYKtFzOQAEAaJ6a6vfvJn+MMQAAAMCWTkABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAICCJg0oTz/9dC644IIcdthh6dmzZ9q0aZOOHTumT58+GTlyZB5++OF3NN/999+fESNGpEePHmnTpk169OiRESNG5P7772/0HMuWLcull16aAQMGZIcddkjHjh3Tt2/fjB49Oi+99NI7/YgAAADAVqCqtra2tikmHjx4cCZNmlQc95WvfCXXXXddWrduXe+Y2tranHbaaRk7dmy9Y0455ZRce+21qaqqqnfMrFmzcvjhh+cvf/lLnfs7deqUm2++OUOGDCmu+52aO3duevbsmSSZM2dOevTosdHfg+an17fv29xLAJrI7IsO39xLAACgDk31+3eTnYEyb968JEn37t1zxhln5Pbbb88TTzyRyZMn51/+5V+y8847J0l++tOfZuTIkQ3Ode6551biyT777JNbbrklTzzxRG655Zbss88+SZKxY8fmu9/9br1zvPHGGxk6dGglnowaNSoPPvhgHnvssZx//vnp2LFjXn311Rx99NGZNm3ae/34AAAAQAvSZGegDB06NMcff3yOOuqobLPNNhvsX7hwYQYNGpRnn302STJp0qTsv//+G4ybOXNm+vbtm5qamvTr1y+TJk1Ku3btKvuXLVuWwYMHZ8qUKamurs6MGTPSu3fvDeY577zz8oMf/CBJcskll2TMmDHr7Z88eXIOOOCA1NTU5KCDDsrvf//79/T5384ZKFsnZ6BAy+UMFACA5mmLOwPl3nvvzTHHHFNnPEmSLl265Mc//nHl59tvv73OcZdffnlqamqSJFddddV68SRJ2rdvn6uuuipJUlNTkyuuuGKDOVavXp0rr7wySdK3b9+cffbZG4wZOHBgTjrppCTJhAkT8tRTTxU+IQAAALC12KxP4TnwwAMr27Nmzdpgf21tbe6+++4kyR577JF99923znn23XfffPjDH06S3HXXXXn7STUPPfRQlixZkiQ54YQT0qpV3R973UuJ7rjjjsZ+DAAAAKCF26wBZdWqVZXtuqLGCy+8ULmXyuDBgxuca+3+uXPnZvbs2evtW/dpPw3N069fv3To0CFJ8sgjjzS8eAAAAGCrsVkDysSJEyvbe+yxxwb7p0+f3uD+da27f93j3sk81dXVlfunvH0OAAAAYOtVvbneeM2aNbnooosqPx9zzDEbjJkzZ05lu3TTl7U3iHn7cev+3KFDh3Tu3Lk4z7Rp07JgwYKsXLkybdq0aXD8WnPnzm1w//z58xs1DwAAAND8bLaAcvnll+eJJ55IkgwfPjz9+vXbYMzrr79e2e7YsWOD86299CZ565HFdc1TmqOueRobUNYNOAAAAEDLslku4Zk4cWK+/e1vJ0m6deuWa665ps5xK1asqGy3bt26wTnXDR3Lly+vc57SHKV5AAAAgK3TJj8D5b/+678yfPjw1NTUpE2bNvnFL36RHXfcsc6xbdu2rWyve8PZuqxcubKy/fZHHa+dpzRHaZ6GvP2yobebP39+BgwY0Oj5AAAAgOZjkwaUF154IYceemgWL16cbbbZJrfcckuDT8XZbrvtKttvvyzn7ZYuXVrZfvulOmvnKc1RmqchpXu0AAAAAFuuTXYJz8svv5yDDz44L7/8cqqqqnL99ddn+PDhDR6zbpQo3aR13TNA3n4/krXzLF26NEuWLGnUPF27dm30/U8AAACAlm2TBJSFCxfmkEMOyfPPP58kueqqq3L88ccXj9tzzz0r2zNmzGhw7Lr7+/bt+67mqampyaxZs+qcAwAAANh6NXlAefXVV/PZz342zzzzTJLkoosuyte//vVGHbvLLruke/fuSd668WxDJk2alCTZeeed06tXr/X27bfffpXthuaZMmVK5RKeQYMGNWqNAAAAQMvXpAFl2bJlOfzww/P0008nSf75n/853/rWtxp9fFVVVYYNG5bkrTNHHn/88TrHPf7445UzS4YNG5aqqqr19h944IHp1KlTkuTGG29MbW1tnfOMHz++sl26vAgAAADYejRZQFm1alWGDx+eRx99NElyxhln5Ec/+tE7nufMM89MdfVb97o9/fTTN3i08PLly3P66acnSaqrq3PmmWduMEfr1q3zzW9+M0kyffr0XHbZZRuMmTx5csaNG5ckGTx4cPr37/+O1woAAAC0TE32FJ4vfOEL+e1vf5sk+fSnP52TTjopf/7zn+sd37p16/Tp02eD1/v06ZPRo0fnoosuypQpUzJo0KB861vfSu/evTNr1qxcfPHFmTp1apJkzJgx2X333eucf8yYMbn11lvz7LPP5pxzzsnMmTNz3HHHpV27dpkwYUIuuOCC1NTUpF27drniiive+x8AAAAA0GJU1dZ3Pct7nfhtl9GUfOhDH8rs2bPr3LdmzZqMGjUq119/fb3Hn3TSSRk7dmxatar/pJqZM2dmyJAhee655+rcv/322+emm27K0KFD39HaG2Pu3LmVpwPNmTPHY4+3Er2+fd/mXgLQRGZfdPjmXgIAAHVoqt+/N9ljjN+LVq1aZdy4cbnvvvsybNiwdO/ePa1bt0737t0zbNiw/OpXv8p1113XYDxJkt122y1Tp07NxRdfnH79+qVz585p3759PvzhD+ess87KtGnTmiSeAAAAAFu2JjsDhfU5A2Xr5AwUaLmcgQIA0Dxt1WegAAAA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AABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFAgoAAAAAAUCCgAAAECBgAIAAABQIKAAAAAAFDRpQHnllVdy77335nvf+14OO+ywdOnSJVVVVamqqsrIkSPf8Xz3339/RowYkR49eqRNmzbp0aNHRowYkfvvv7/RcyxbtiyXXnppBgwYkB122CEdO3ZM3759M3r06Lz00kvveE0AAABAy1fdlJPvuOOOG2We2tranHbaaRk7dux6r8+bNy933nln7rzzzpxyyim59tprU1VVVe88s2bNyuGHH56//OUv670+Y8aMzJgxI9ddd11uvvnmDBkyZKOsGwAAAGgZNtklPD179syhhx76ro4999xzK/Fkn332yS233JInnngit9xyS/bZZ58kydixY/Pd73633jneeOONDB06tBJPRo0alQcffDCPPfZYzj///HTs2DGvvvpqjj766EybNu1drRMAAABomZr0DJTvfe976d+/f/r3758dd9wxs2fPzi677PKO5pg5c2YuueSSJEm/fv0yadKktGvXLknSv3//HHHEERk8eHCmTJmSiy++OCeeeGJ69+69wTyXXXZZZsyYkSS55JJLMmbMmMq+gQMH5qCDDsoBBxyQZcuW5cwzz8zvf//7d/uxAQAAgBamSc9A+cEPfpChQ4e+p0t5Lr/88tTU1CRJrrrqqko8Wat9+/a56qqrkiQ1NTW54oorNphj9erVufLKK5Mkffv2zdlnn73BmIEDB+akk05KkkyYMCFPPfXUu14zAAAA0LI066fw1NbW5u67706S7LHHHtl3333rHLfvvvvmwx/+cJLkrrvuSm1t7Xr7H3rooSxZsiRJcsIJJ6RVq7o/9ro3tr3jjjve4+oBAACAlqJZB5QXXngh8+bNS5IMHjy4wbFr98+dOzezZ89eb9/DDz+8wbi69OvXLx06dEiSPPLII+9myQAAAEAL1KT3QHmvpk+fXtneY489Ghy77v7p06evd6+Vxs5TXV2d3r17Z9q0aesd0xhz585tcP/8+fPf0XwAAABA89GsA8qcOXMq2z169GhwbM+ePes8bt2fO3TokM6dOxfnmTZtWhYsWJCVK1emTZs2jVrruu8PAAAAtCzN+hKe119/vbLdsWPHBseuvfQmeeuRxXXNU5qjNA8AAACwdWrWZ6CsWLGist26desGx657psjy5cvrnKc0R2mehrz9rJe3mz9/fgYMGNDo+QAAAIDmo1kHlLZt21a2V61a1eDYlStXVrbf/qjjtfOU5ijN05DSJUYAAADAlqtZX8Kz3XbbVbZLl9MsXbq0sv32S3XWztOYS3IamgcAAADYOjXrgLLuWR2lp9ysewnN22/ounaepUuXZsmSJY2ap2vXro2+gSwAAADQsjXrgLLnnntWtmfMmNHg2HX39+3b913NU1NTk1mzZtU5BwAAALD1atYBZZdddkn37t2TJBMnTmxw7KRJk5IkO++8c3r16rXevv3226+y3dA8U6ZMqVzCM2jQoHezZAAAAKAFatYBpaqqKsOGDUvy1pkjjz/+eJ3jHn/88cqZJcOGDUtVVdV6+w888MB06tQpSXLjjTemtra2znnGjx9f2R4+fPh7XT4AAADQQjTrgJIkZ555Zqqr33pY0Omnn77Bo4WXL1+e008/PUlSXV2dM888c4M5WrdunW9+85tJkunTp+eyyy7bYMzkyZMzbty4JMngwYPTv3//jfkxAAAAgC1Ykz7G+JFHHsnMmTMrPy9cuLCyPXPmzPXO+EiSkSNHbjBHnz59Mnr06Fx00UWZMmVKBg0alG9961vp3bt3Zs2alYsvvjhTp05NkowZMya77757nWsZM2ZMbr311jz77LM555xzMnPmzBx33HFp165dJkyYkAsuuCA1NTVp165drrjiivf82QEAAICWo6q2vutZNoKRI0fmxhtvbPT4+payZs2ajBo1Ktdff329x5500kkZO3ZsWrWq/6SamTNnZsiQIXnuuefq3L/99tvnpptuytChQxu95saaO3du5elAc+bMWe8JQ7Rcvb593+ZeAtBEZl90+OZeAtBEfH9Dy+X7e+vQVL9/N/tLeJKkVatWGTduXO67774MGzYs3bt3T+vWrdO9e/cMGzYsv/rVr3Ldddc1GE+SZLfddsvUqVNz8cUXp1+/funcuXPat2+fD3/4wznrrLMybdq0JoknAAAAwJatSc9A4X85A2Xr5F+woOXyL1jQcvn+hpbL9/fWYas+AwUAAABgcxJQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKNgiAkpVVVWj/jvwwAOLc91///0ZMWJEevTokTZt2qRHjx4ZMWJE7r///qb/IAAAAMAWaYsIKBtDbW1tTj311Bx22GG58847M2/evKxatSrz5s3LnXfemcMOOyynnnpqamtrN/dSAQAAgGamenMv4J346le/mq997Wv17u/QoUO9+84999yMHTs2SbLPPvvknHPOSe/evTNr1qxccsklmTp1asaOHZuuXbvmRz/60UZfOwAAALDl2qICSrdu3fLRj370HR83c+bMXHLJJUmSfv36ZdKkSWnXrl2SpH///jniiCMyePDgTJkyJRdffHFOPPHE9O7de6OuHQAAANhybRWX8Fx++eWpqalJklx11VWVeLJW+/btc9VVVyVJampqcsUVV2zqJQIAAADNWIsPKLW1tbn77ruTJHvssUf23XffOsftu++++fCHP5wkueuuu9wLBQAAAKho8QHlhRdeyLx585IkgwcPbnDs2v1z587N7Nmzm3ppAAAAwBZii7oHym233ZZbbrklL730Uqqrq/OBD3wgn/rU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CgAAAECBgAK0CC+//HK+/e1v5+/+7u/SqVOntG7dOh/4wAfysY99LF/4whcyfvz4vPbaa+sd8/an1kyYMCFHHnlkunfvnnbt2qVv37754Q9/mKVLl6533K9+9asMGTKkMm7PPffMhRdemFWrVtW7vlWrVuWee+7JN77xjfTv3z/ve9/7su222+b9739/PvnJT+a8887LwoULN/qfCwBsydasWZPf//73GT16dAYNGpQuXbpk2223TefOnbP33ntn9OjReemllxqc4+1PsXvuuefyjW98I7vvvnvat29f59N/pk2blq985SvZeeed07Zt23zwgx/Ml7/85Tz99NNJkpEjR6aqqiq9evVq8L0XL16cH/3oRxk4cGC6dOmSNm3apHv37hk2bFjuuOOOd/vHAmwutQBbuEmTJtVuv/32tUka/O+ee+5Z77i1r3//+9+vvfDCC2urqqrqPO5Tn/pU7euvv167Zs2a2jPOOKPe+T/3uc/V1tTU1LnGE044obi+97///bWPPPJIvZ9z8ODBtUlqBw8eXOf+dT8PAGwpbrjhhsp32AsvvLDevu9///vF78/27dvX3nHHHfXOv+7351133VXboUOHDeZY933Hjx9fu+2229b5Xttuu23t+PHjK9/rH/rQh+p93/vuu6+2c+fODa798MMPr3399dff458gsKlUb5wMA7B5rFy5Mscdd1xee+21bLfddvnqV7+agw46KN26dcvq1avz4osvZvLkyfnlL39Z7xy//vWv88QTT2TgwIE5/fTT06dPnyxcuDBXXnllfv3rX+exxx7LRRddlB122CFXXnllDjvssJx88snp1atX5s6dmwsvvDCPP/547r///vzbv/1bTjvttA3eo6amJrvuumuGDx+eAQMG5IMf/GCqq6vz4osv5oEHHsj111+fRYsWZfjw4fnzn/+cbt26NeUfGwBsEWpqarLTTjtl+PDhGThwYHbddde0bds2c+bMyWOPPZaf/OQneeONN/LFL34xTz/9dPr27VvvXC+99FK+/OUvp3379vnud7+b/fffP9tss02efPLJdOzYMUnyyCOP5B/+4R+yZs2atGvXLmeddVY+97nPpU2bNpkyZUouvPDCnHLKKfnIRz7S4Lp/97vf5Ygjjsibb76ZXr165atf/Wo++clPZvvtt8+8efNy66235mc/+1nuu+++nHDCCQ3+PQVoRjZ3wQF4Lx588MF6zzBZ1+rVq2tfffXV9V7LOv8CdNRRR21w9khNTU3tvvvuW5ukdrvttqtt27Zt7ZlnnrnB3EuXLq390Ic+VJukdq+99qrz/WfOnFm7Zs2aetc3bdq02o4dO9YmqT333HPrHOMMFABaoobOQHnhhRdqV61aVe+xc+bMqd15551rk9R++ctfrnPM2u/PJLXdu3evffHFF+ud7+Mf/3htktrWrVvXPvrooxvs/9vf/la76667Vuar6wyUN954o3bHHXesTVJ76KGH1i5durTO9xo7dmxlngceeKDeNQHNh3ugAFu0v/71r5XtAw44oN5x1dXV2X777evc1759+4wdOzbbbLPNeq9vs802OfXUU5Mkr7/+erp27ZpLLrmkzuNPOOGEJG9dM/3qq69uMKZ3796pqqqqd30f+9jHcvLJJydJ7rrrrnrHAcDWpFevXtl2223r3d+jR4+MGTMmSfIf//Efqa2tbXC+iy66KB/84Afr3Pf444/nj3/8Y5Lk61//ej71qU9tMKZbt265/PLLG3yPG264IX/729/Stm3b/PSnP0379u3rHDdq1KgMGDCgcgzQ/LmEB9ii7bTTTpXtG264IWecccY7nuOQQw7JDjvsUOe+vfbaq7I9YsSIev8S9/GPf7yy/cILL2Tvvfdu8D0XL16c//7v/86KFSsqf9nr3LlzkuSZZ57J6tWrG/wLIwBsjV577bUsWrQoy5Ytq3x/rg0Ur732Wl544YXsuuuudR7bunXrHH300fXO/eCDD1a21/7DSF0OP/zwvP/978+iRYvq3H/33XcnSQYPHly8JPeAAw7IE088kcmTJzc4DmgeBBRgi7bffvtl1113zfPPP58zzzwzN910U4YPH57BgwenX79+ad26dXGOPn361LtvbdR4J+Nef/31Osf86U9/yuWXX55f//rX650583Zr1qzJ4sWL3QcFAJK8+OKLueyyy3LPPffkxRdfbHDswoUL6w0ou+++e9q2bVvvsX/+85+TJG3atMlHP/rResdts8022XvvvdcLLuuaMmVKkuQ3v/lNg2efrquhvxcAzYeAAmzRtt1229xzzz35/Oc/n+nTp+fJJ5/Mk08+mSRp165dBg8enK985Ss59thjN7hEZ636Tq1NklatWr3jcW+++eYG+8eNG5fTTjstNTU1xc+UJMuXL2/UOABoyX7961/n85//fJYtW9ao8Q19f77vfe9r8NjFixcnSXbYYYd6/86wVteuXet8ffXq1VmyZEnDi6xDYz8fsHm5Bwqwxdtzzz3zpz/9KXfeeWf+4R/+Ib17907y1l+i7r///nzpS1/KJz/5ybzyyiubZX0zZsyoxJNu3brl0ksvzVNPPZVFixZl1apVqa2tTW1tbcaNG1c5pnQNNwC0dIsWLcoXv/jFLFu2LB07dsx5552XyZMn55VXXsnKlSsr35/rngnS0PdnKYpsDOv+I8oxxxyTP/3pT43+D2j+nIECtAjbbLNNjjzyyBx55JFJkvnz5+fXv/51fvKTn+Spp57KU089lVNPPTV33nnnJl/b+PHjU1NTk2222SYPPfRQvY9YXPsvXwBActttt1XO5rjjjjtyyCGH1DluY31/rj1D5b//+7/z5ptvNhhcFixYUOfrbdu2Tfv27bNs2bIsWbKkwUuBgC2PM1CAFmmnnXbKP/zDP2Ty5Mn5u7/7uyTJvffeu1kujfmv//qvJG/daLa+eJL87zXTAMD/fn/usMMO9caTZON9f37kIx9JkqxcubLBM0LefPPN/Od//me9+/fZZ58kyaOPPurSHGhhBBSgRdt2220zePDgJElNTc27ui75vVp735OG/hL117/+tXLXfgDgf78/V65cmTVr1tQ5ZtmyZfn3f//3jfJ+n/nMZyrbDc1533331fsEniQ54ogjkiRLly7N1VdfvVHWBjQPAgqwRXv44Yczc+bMevevWrUqEydOTJJ07Nix3pu+NaXdd989SfLss8/m8ccf32D/smXL8sUvftGNYwFgHWu/P5cuXZrbb799g/1vvvlmTj755Lz88ssb5f0GDhyYvfbaK0ly9dVX57HHHttgzIIFC3LWWWc1OM9pp52WLl26JEm++93v5te//nWD4x999NFMmjTpXa4a2JQEFGCL9uCDD+bDH/5wDjzwwFx66aX5zW9+k6effjqPPvpobrjhhuy///55+umnkyQnn3xyqqs3/a2fvvKVryR56/HEQ4YMyUUXXZRJkybliSeeyDXXXJO99947EyZMyKBBgzb52gCguTrmmGPSpk2bJMnIkSPzne98J7///e8zZcqU3HjjjfnkJz+ZW265ZaN+f1599dVp1apVVq1alYMPPjjnnntuHnnkkTz55JO55ppr8olPfCJz5szJ3nvvnSR1PqZ4++23zy233JLq6uqsXLkyQ4cOzTHHHJNbb701U6ZMyZQpU3LPPffkvPPOy8c//vHst99+mTZt2kb7DEDTcRNZYIu3Zs2aTJw4sXKmSV1GjBiRCy+8cBOu6n/1798/P/jBD/L9738/ixcvzj/90z9tMObss8/ORz/60Tz66KObYYUA0Pz06NEj11xzTU4++eQsX748F1544Qbf5ccee2xGjRqVgw8+eKO853777Zfrr78+o0aNyvLly3P++efn/PPPr+yvrq7ONddck0mTJuU///M/07Zt2zrnOfjgg/Ob3/wmX/rSl/LXv/41t912W2677bZ633f77bffKOsHmpYzUIAt2jnnnJNf/epXOeuss7Lvvvvmgx/8YNq2bZu2bdumV69eOfbYY3Pffffll7/8Zb1/ydkUvve97+W+++7LoYcemve9731p3bp1evTokREjRuS3v/1tLrvsss22NgBork488cQ8/PDDOfLII9O1a9dsu+222WmnnfK5z30ut956a37+859v9McTn3DCCZkyZUq+9KUvpXv37mndunV23nnnHHPMMXnkkUdy8skn57XXXkuSdOrUqd55Pv3pT2fWrFn5v//3/+Zzn/tcdtppp7Ru3Tpt27ZNz549c+ihh+b888/PjBkzcvzxx2/UzwA0jarahh6WDgAAwHp22223zJo1K1/+8pfz05/+dHMvB9hEnIECAADQSE8++WRmzZqVJNl3330382qATUlAAQAA+B8NPd1v0aJFGTVqVJKkTZs2OfbYYzfVsoBmwE1kAQAA/schhxySXXbZJcOHD89ee+2VTp06ZfHixXn00Ufzk5/8JPPnz0+SnHvuuZXHFQNbB/dAAQAA+B+9evXKiy++2OCYr33ta7nqqqvSqpUT+mFrIqAAAAD8j4kTJ+aee+7JxIkTM3/+/CxcuDDV1dX5wAc+kP322y+nnHJKPvWpT23uZQKbgYACAAAAUOCcMwAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFAAAAIACAQUAAACgQEABAAAAKBBQAAAAAAoEFACgWVq4cGHGjBmTPn36pF27dtlxxx1zyCGH5M4770ySjB8/PlVVVamqqsrs2bPXO7ZXr16pqqrKyJEjkyRPPfVURo4cmV122SVt2rRJVVXVBu/3pz/9Kaecckp23333tG/fPtttt10+8pGP5Kyzztpg/nU99NBDlXU89NBDDX6mtePOO++8Dfadd955lf1JsmTJknz/+9/PRz7ykXTs2DE77LBDDjzwwNx0000NvgcA0DSqN/cCAADe7o9//GMOOeSQLFiwoPLaihUr8sADD+SBBx7IKaeckoEDBzZqrmuvvTann356ampq6h1z4YUX5txzz82aNWvWe/2ZZ57JM888k2uuuSZjx47N8ccf/+4+0Dv0wgsv5JBDDsmsWbMqry1dujQTJ07MxIkTc9ddd+WWW25JdbW/ygHApuJbFwBoVhYvXpzPfe5zlXjypS99KV/+8pfTtWvXzJw5M1deeWXGjh2bP/7xj8W5nnzyyfzsZz9Lz549M3r06HziE5/Im2++mYcffrgy5ic/+Um+853vJEm6du2ab33rWxk0aFDefPPNPPDAA7n00kuzdOnSjBw5Ml26dMmQIUOa5oOv49hjj80LL7yQ0047LZ///OfTqVOnTJs2LRdffHGeffbZ3H777dlpp53yr//6r02+FgDgLQIKANCsnHfeefnrX/+aJLnsssty9tlnV/Z94hOfyOc///kcddRRufvuu4tzPfPMM/nYxz6WSZMmpXPnzpXXBw0alCRZsGBBxowZkyTp3r17Hn/88fTs2XO9cUcccUT233//LF26NKecckpeeOGFbLvtthvjo9brySefzM0335wvfOELldf69euXo48+Ovvvv3/++Mc/5uqrr86oUaPysY99rEnXAgC8xT1QAIBmY8WKFbnxxhuTJH/3d3+Xf/zHf9xgzDbbbJP/9//+X9q2bduoOa+++ur14sm6brjhhixbtixJ8uMf/3i9eLLWPvvsk3/6p39KksybNy933XVXo973vRg6dOh68WSt7bbbLmPHjk2SrFmzJtdee22TrwUAeIuAAgA0G0899VReffXVJMnxxx9f581ek2THHXfMZz/72eJ8PXv2zP7771/v/gceeCBJ0rlz5xx11FH1jjv55JM3OKYpnXjiifXuGzBgQD7ykY9ssrUAAG8RUACAZuPPf/5zZfsTn/hEg2P79etXnG+vvfZq1Pvts88+DV6Ws+OOO6ZXr14brLGp9O/fv8H9AwYMSJI899xzWbVqVZOvBwAQUACAZmTx4sWV7W7dujU4tmvXrsX53ve+9zW4/7//+7+TvBVISj7wgQ+sd0xTKn32teutra1d788MAGg6AgoA0GJts802jRpX36VC66qtrX2vy2m00no25VoAgLcIKABAs7HuGSOvvPJKg2PXPub4vdhhhx2SpPLUn4b87W9/W++YtVq1+t+/Tq1Zs6be45cuXdroda19r/qs/bOpqqoqnmUDAGwcAgoA0GysvTlqkkyZMqXBsaX9jfHRj340STJ16tSsXr263nGvvPJKXnzxxfWOWWu77barbDd0Oc1f/vKXRq/rySefbNT+3XffPa1bt270vADAuyegAADNRr9+/dKpU6ckyU9/+tN6L1X529/+lt/85jfv+f0OPvjgJMmSJUvyy1/+st5x48aNq6xl7TFr7bLLLpXthqLOzTff3Oh1rX2Uc12mTJlSuZHt29cCADQdAQUAaDbatm2b448/Pkny9NNP51/+5V82GLNmzZqceuqpWbFixXt+vxNPPDHt27dPkpx99tmZM2fOBmP++Mc/5oILLkiS7LzzzjnyyCPX29+5c+fK035uuOGGOm8yO2nSpPzrv/5ro9f1H//xH/nFL36xwetvvPFGTjnllCRvXTp06qmnNnpOAOC9EVAAgGblvPPOqzzxZvTo0fnyl7+c3/zmN3n66afzi1/8Ivvvv3/uvvvuyqN8k8bdBLYuXbt2zaWXXpokefnll9OvX79cfvnl+cMf/pDHHnss/+f//J/st99+eeONN1JVVZWxY8fW+bjjr33ta0neOjNm//33z89//vNMnTo1Dz74YM4666wceuihjXrs8lr9+vXLF7/4xXz961/PhAkT8tRTT+WGG25Iv379MnXq1CTJ17/+9eJjmgGAjad6cy8AAGBdO+ywQ+6///4ccsghWbBgQW666abcdNNN640ZOXJk9t9//zzxxBNJ3jpz5d362te+liVLluS73/1uXnnllfzjP/7jBmPatGmTsWPHZsiQIXXOMWrUqNx///2566678swzz+QLX/jCevs/+tGP5pe//GW6d+/eqDX94he/yGc+85n85Cc/yU9+8pMN9h911FF1np0DADQdZ6AAAM3Oxz/+8TzzzDM5++yzs/vuu6dNmzbp0qVLDjrooNx888254YYb8tprr1XGr71vyrv1ne98J1OnTs2oUaPSu3fvtGvXLh06dEjfvn1zxhlnZMaMGZVLi+rSqlWr3H777bn66qvTv3//dOjQIR06dMhee+2V888/P3/4wx+y0047NXo9u+yyS5566ql85zvfSd++fdO+fft06tQpBxxwQH72s5/l9ttvT3W1fwcDgE2pqra+u7MBADRjJ598csaNG5cePXrUee+SLc15552XH/zgB0lS781zAYDNxxkoAMAWZ/ny5bn77ruTJPvuu+9mXg0AsDUQUACAZmfWrFn1noXx5ptv5qtf/WoWLlyYJDnhhBM25dIAgK2Ui2cBgGbnhz/8YZ544okcd9xx+eQnP5lu3bpl+fLlmTZtWv7t3/4tTz/9dJLkM5/5TA4//PDNvFoAYGsgoAAAzdL06dPz/e9/v979gwYNyq233vquH2EMAPBOCCgAQLPzT//0T+nTp09+97vf5cUXX8yCBQuyevXqvP/970+/fv1y7LHH5rjjjkurVq5GBgA2DU/hAQAAACjwzzYAAAAABQIKAAAAQIGAAgAAAFAgoAAAAAAUCCgAAAAABQIKAAAAQIGAAgAAAFAgoAAAAAAUCCgAAAAABQIKAAAAQIGAAgAAAFAgoAAAAAAUCCgAAAAABQIKAAAAQIGAAgAAAFAgoAAAAAAUCCgAAAAABQIKAAAAQMH/Bz+2cEnnbs6vAAAAAElFTkSuQmCC"/>

cf) 히스토그램과 막대그래프

1) 데이터 유형

- 히스토그램: 연속적인 수치 데이터를 다룹니다. 히스토그램은 변수의 분포를 보여주며, 일반적으로 수치적 데이터의 빈도수 또는 빈도 분포를 나타냅니다.

- 막대그래프: 범주형 데이터를 다룹니다. 각 범주는 서로 독립적이며, 각 범주의 빈도수나 양을 비교하는 데 사용됩니다.



2) 축

- 히스토그램: 수평축(x축)은 변수의 구간을 나타내며, 수직축(y축)은 빈도수 또는 밀도를 나타냅니다.

- 막대그래프: 수평축(x축)은 개별 범주를 나타내며, 수직축(y축)은 그 범주의 빈도수나 양을 나타냅니다.


# <span style="color:blue; font-weight:bold;">The End of Note</span>

