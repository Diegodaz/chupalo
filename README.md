# chupalo
{
  "cells": [
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "view-in-github",
        "colab_type": "text"
      },
      "source": [
        "<a href=\"https://colab.research.google.com/github/anoblega-unsa/Parcial1/blob/main/EDA_Parcial1.ipynb\" target=\"_parent\"><img src=\"https://colab.research.google.com/assets/colab-badge.svg\" alt=\"Open In Colab\"/></a>"
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Parcial 1 - Algoritmos y Estructura de Datos\n",
        "\n",
        "Indicaciones: Después de terminar su evaluación, llenar el siguiente formulario con sus respuestas: https://forms.gle/UWej2ueqApBMBMjm6\n",
        "\n",
        "**Nombre Completo:Diego Alonso Zanabria Sacsi**\n",
        "\n",
        "**CUI:20192274**"
      ],
      "metadata": {
        "id": "OJ7SVwcSYVAS"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "Parte 1: Dado que una lista enlazada puede representar un polinomio como lo muestra la imagen, se requiere lo siguiente:\n",
        "\n",
        "\n",
        "\n",
        "1.   Implementar los métodos de la clase **Polinomy** para que las inserciones sean ordenadas de acuerdo al exponente del termino, esto de mayor a menor (de izquierda a derecha) y  sin repeticiones de términos con el mismo exponente, es decir, si tengo dos términos con el mismo exponente estos deben combinar (4x^2 + 6x^2 = 10x^2). \n",
        "  \n",
        "  **Nota**: Solo considerar que los coeficientes serán valores positivos para evitar mayor complejidad.\n",
        "\n",
        "2.   Que la clase soporte la operación de dos polinomios p1 y p2, y que nos consiga retotar un nuevo polinomio p3.\n",
        "\n",
        "3.   La clase debe poder evaluar el resultado final al reemplazar su variable independiente, es decir, x = 10 -> 2x^2 + 3x + 1 = 231.\n",
        "\n"
      ],
      "metadata": {
        "id": "Ege6UEjrL5FG"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "Parte 1:\n",
        "![Untitled Diagram-Page-3.drawio.png](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAApUAAADGCAYAAACD1HvXAAAAAXNSR0IArs4c6QAAEcB0RVh0bXhmaWxlACUzQ214ZmlsZSUyMGhvc3QlM0QlMjJhcHAuZGlhZ3JhbXMubmV0JTIyJTIwbW9kaWZpZWQlM0QlMjIyMDIyLTEwLTA5VDIzJTNBNDQlM0E0OS44ODdaJTIyJTIwYWdlbnQlM0QlMjI1LjAlMjAoTWFjaW50b3NoJTNCJTIwSW50ZWwlMjBNYWMlMjBPUyUyMFglMjAxMF8xNV83KSUyMEFwcGxlV2ViS2l0JTJGNTM3LjM2JTIwKEtIVE1MJTJDJTIwbGlrZSUyMEdlY2tvKSUyMENocm9tZSUyRjEwNS4wLjAuMCUyMFNhZmFyaSUyRjUzNy4zNiUyMiUyMGV0YWclM0QlMjJHMDBxSEt3TVlKY201V1pESU4ycCUyMiUyMHZlcnNpb24lM0QlMjIyMC40LjAlMjIlMjB0eXBlJTNEJTIyZ29vZ2xlJTIyJTIwcGFnZXMlM0QlMjIzJTIyJTNFJTNDZGlhZ3JhbSUyMGlkJTNEJTIyRlp4T0cyZzRfV0YyMTN6WTNSeGglMjIlMjBuYW1lJTNEJTIyUGFnZS0xJTIyJTNFM1ZmYmNwc3dFUDBhSHBQaFlnRjV0SjI0Zldnbm5Va25iWjg2TWl5Z2lZeW9FRGJ1MTFjQ2NjZTVqWlBPNU1GanRDc3RxejFuajRUaHJIZmxKNDZ6NUNzTGdScTJHWE1TR3M2MVlkdVclMkZFbERobU1ZR05TTU8lMkZLM01acmFXcEFROHNGRXdSZ1ZKQnNhQTVhbUVJaUJEWFBPRHNOcEVhUFROTzRDVEdGaSUyRlVGQ2tkUldINW1kJTJGVE9RT0dsZVpKbmFzOFBOWkczSUV4eXlROCUyRmszQmpPbWpNbTZxZGR1UWFxS3RQVXBWNjNPZUZ0RSUyQk9RaXVjczJDVExaRVBTdUhpNFQ1Yk83NjEzZXg5ZDZDaDdUQXU5WWNOMnFZeTNpcGdNSzdNV1IxMEs5MCUyRkJHc2RGWHVHeWxCT3NSVlpLYSUyQmVYVDdINjN4UnBJQWhMbTRBeXN6cG03ZFpGYWNQYm5CVnBDQ3BaUzdvUENSRndsJTJCRkFlUSUyQlNPTktXaUIzVjdvaFF1bWFVOFdxdEV5THd3NFcwNTRLekIlMkJoNWZIdnJ1Rzc3dmoxd0FlWEpDbG90THBLdHdIWWclMkJGRk8wUXZzS3czbHNSNjdlbmpvaUdFNzJwYjBTZEZRQUd2dXhXM29EaSUyRjVvQ0Y3QVh6MkJMN2JRbVNGT0d0eG95aXlnMkN1dUtHN2RkR1ppcnR3aDhXMTBMUzZiWFAxcTR2ZXFyak9URyUyQk15Z3BwdUZTYUlrY0J4WGxPZ21FbHU3S2J1bk8wb0ZtS3JGQVM4VlBQVk0lMkIlMkYxTHhMcEVmWHBWNVdEWTVOakJFMmZnRHoyR3g5dEVCbTYybkVxME1Md25pc2NTT3M1Rlpad1FONFNqJTJCbW1QWXdRNDlBeG9GaVFmYkROT1p3MUclMkY0eGtnbFNwb3lyaldpakRXaVFwMiUyQlh0V1h4bEVnenh3RkdqZXN3RHdHTVFsVTBhcmQ5dXVadHBnd0xZVlM1U2R3JTJGakFsblFUdUM5N0tVM1RBTlV4Sm5Db2lTaEJCa21DbDJwSElrMnlwSFRzU2hpckdpb09VYjd5dDRpbUdaR3BmMVU3UnlrRFhNMHc5MmQlMkY2bE5YQnVzT3V6NlhUelhWU0RNeEwlMkJ5d011YkQ4NFJJV1JUbThDWWJvdmRUQ2ZMMWFnQ1VQU205T0xhNWN6OEh1aDFhTDBlRXRtJTJGNTFZdEVlVFA5SkxOd0owVElPJTJCdzh0RnVncHNmQ3N4Vms0WWwlMkI5bDF4NE0zTHh3b3UzZiUyQkxpJTJGYjNpd2ZNdTNVS2RNd05tREtVaFpTbU1kRVNibnMlMkJndWR2bTQxSjNodXVrNDZGaHUwOXZrJTJCNk0xamd2djB6S1lmY1JWOU9qJTJCODUxYnY0QiUzQyUyRmRpYWdyYW0lM0UlM0NkaWFncmFtJTIwaWQlM0QlMjJMUEd3NXUzZFdYQXFQOWtDMjR2bCUyMiUyMG5hbWUlM0QlMjJQYWdlLTIlMjIlM0U1VnBMYzVzd0VQNDFQaVlEQ0RBY0V5ZHREODAwblhTUzVxaUFiSWd4WW9TSTdmNzZDaU5la3ZHRGdFbWNRMmJZWllXbDNlJTJGYlhUYU13R1N4JTJCazVnNU4xaEZ3VWpUWmtSM3gyQm01R21xZXlQS1NJNFF6VkZhdkhnJTJGOHVWQ3RjbXZvdmltaUhGT0tCJTJCVkZjNk9BeVJRMnM2U0FoZTFzMm1PSkMzOGVEQUFFbmFKOSUyQmxYcWExREtYVSUyRjBEJTJCek10JTJGU0ZYNG5RWE1qYmtpOXFDTGx4VVZ1QjJCQ2NHWVpsZUwxUVFGcVdkeXYyVHJ2alhjTFRaR1VFZ1BXVENseThmWEozWCUyQmUlMkZXY1hNMGZyJTJCOWVvNHNMZyUyQiUyQk5ydk1ESTVlZG40dVlVQSUyRlBjQWlEMjFKN1RYQVN1aWg5cXNLazB1WW54aEZUcWt6NWlpaGQ4OWpCaEdLbTh1Z2k0SGRqU3ZDOGNHZXFtZUtRY25QVlluSzJxM1FyallmbHFoZ254RUU3VHBoakJKSVpvanZzUUJFU0JsU0VGNGlTTlZ0SFVBQ3AlMkYxYmZCJTJCUVltaFYycGQlMkZaQlhmOUVXSGd6MzJEUWNKJTJGNlElMkJNNTB5alN2RmhNSXJTeTRoZ0I4VnNJOWRMejZmb0lZSWJOeXdaeCUyQnJlZm9IT2ZMYUoyYSUyQkVCbjZJR253JTJCOVlOZ2dnTk1OcjhEWEFOWnJsNUVxM0xIMGw2QWFSWlJla09Fb3RYdU9NbCUyQnpSZFluQjNyVEFZNXpaY2wyZFNjUVY2RmFLYlNVeWpHTFJqUmdnUE1QMlQ5TiUyQlhRcFpHTHo5VjdOeXRPc0V4YWMyayUyRmQlMkJyMGRHSHNiUVJWRHZIVWNwRGpiQXZ4aTJYb2h0SXRFYlVURVhHejlJb1F1SzRZUk5nUGFWeDU4bjJxS0hISU1ub2RoN2FRVEFWN1hjUnQzWjVkWkRzb2NWZ2NwVDAwTlNsTE1FWkhDWlVRVzBKQTNaOGZSRkJNcDlwMlVMam1pMmwweEh2TkVQeG55THdmYjZFOTZJdjI1aENGc0VnQ2FqVUZLSmVhOGU0czBDRnh3WUhFYlloNHY4UUZwZ0FremRoSjNEMzIlMkZSQlhQZjgyNjFDUTJFTzJXYUNwemRMT3ZNM1N0WSUyRldacW4yb0FtMzg2N3IlMkJOYXExcGwxeUVUOVJFeHNsYTROc0xOdmt1ekhJbkJQMFdmcDU5Tm42ZllINjdQVVlSc3RaVlJydEQ1VW4yVWYybWRwUTlaUXU2bUdnak92b2FiWU9RNWVRNHZKNGttNVZLdGJmUlRHRGltVmg2aCUyRlRyV3FodVB4Y2RYUUZ0JTJCYVQxRU5jeCUyQmVRemtjaSUyQjNINE9WUUh2Q2U1ZHpoc0c3MG9GQWVSMG1aUThyMkFVRHhpQ3lwOEZWbGVJJTJGbHRxVWZONWpZWTk4VHQ5dE11eiUyRlhZS0tiekM2RlMxWEVDYkF1NUlnTThoS09PZ3VkUEEzJTJCSW8yWUpiN1RETjZJcWZKZzZkT1dTRnRzY3djdmtmclhLSkg5bHo3cERVYU1XVVBwazZjNFlxMFNIOVNRJTJCNDZ0b2FaWXE4SHUlMkZuaVBmVTgxMUpMSUx3TTJkSyUyRlNiMCUyQlk1QVF3am4ybmpyWTZYUGREcUdtZUFRRFlBOCUyQk5kSSUyQkl6NDZOQ0ZjZVhtN2IlMkZoT29ranlNTGNrajE3MjdLTmZqcjFrdEFhNEtMMXBTZHVzSTRPS0dUd0xZM0s4bkJlektwd1ZlMlhWbCUyRk1ha0VxdXBzRDRhbFlkOUJEUVVLc1YyeFc0TFNoRXNuWFdjVEN5JTJGUTh2TXkwJTJGMXdPMSUyRiUzQyUyRmRpYWdyYW0lM0UlM0NkaWFncmFtJTIwaWQlM0QlMjJMNFFhNjZCUGtnMWZxY19FZmVycSUyMiUyMG5hbWUlM0QlMjJQYWdlLTMlMjIlM0U1VmxiYjlvd0ZQNDFrYmFIVnJrRGp4UjZXZFZLayUyRnF3ZFMlMkJUU1V5U3pjU1pZeURwcjU5Tm5Lc0REVkJLMWtrSXhaJTJCUGIlMkJlYzc3T2RLTVpra2R3U0VQbVAySVZJMFZVM1VZeXBvdXNqMDJiJTJGSEVnendES3REUEJJNEdhUVZnSlB3UXNVb0NyUVplREN1R1pJTVVZMGlPcWdnOE1RT3JTR0FVTHd1bTQyeDZnJTJCYWdROEtBRlBEa0F5JTJCaTF3cVolMkJoUTBzdDhUc1llSDQlMkJzcWFLbWdYSWpRVVElMkI4REY2d3BrWEN2R2hHQk1zNmRGTW9HSSUyQnk3M1M5YnVaa3R0TVRFQ1E5cWx3ZXFuUGNhT1BwN0ZqNlA3SDZNdjklMkJUbTlrSUVJNlpwdm1Eb3N2V0xJaWJVeHg0T0Fib3UwU3VDbDZFTGVhOHFLNVUyRHhoSEROUVklMkJBdFNtb3BnZ2lYRkRQTHBBb25hbUJMOHUzQW5SJTJCWTRwTUpjRzdKeU5pcyUyQmxhMkxGVkNNbDhTQk8xYVlKdzBnSHFRNzdQUWlKQ3lWSVY1QVNsTFdqa0FFYUxDcXp3T0lwUElLdTlMdjdFRzRmbzh3aUg1WEFDM0ZTSjlZWkNibVp5azhwZk81MzlaJTJCUU9GVEJEWWVXRE1DMWgzZDd0WVZKQlFtdXgwck95SnZZSXQwVG91RXo4cnJraDFhbnZKJTJCaFJsNXV6ZjNuWDJPRkdiZUl1bDMwWDVUZU9hRlN5c3ZUcE5xNVRRVnBYZE5mYjFqNmh2blRQM2hoMWVncm1IWVFyek9ZZGcwSFJNQzBvcEJoSU9ReHBXZXYzS2c1TE9oTmZoc05IYVIlMkZlelpRemFETWlHS3BSeWVJN29zandNbWozciUyRjVORXclMkJ5YVBndyUyRlBMNk1qdjh4enl0em9yTHVVMXVOZHFtdjRqajJnSFNTUFp2TzQ4eDV5WjhoeXg2Q0oxaiUyQjVzJTJGUyUyQnlWMCUyQmdRJTJCc2Q4ZnFXSHVtMjgyZHkyaUVLQ09vYUZWR2FWOUdiUnZucEl3eVpVWXhhS0wyajFFRHRYZU1raSUyQm5Nc1ZDZDh4ZnRyQ1NnMEFjQjA3ZFVYV0N2YzZXOG5wVjdsWFB0YTJxZmVQcXpySkRUJTJCT1ZNRmd0VWNpeEk4bW9OM1RWYkFRMzB3aUppMUklMkZXb05zdzI2Y2ZpdmFhZkxCJTJGUTRDdDFXaEg4QU1vbnJXQUJSNElVOHBGanhJR01DWkZUZ0FqVVhGSW5EZFRNQmhITHlBMmFZJTJGbmdkQ2hGam4xcFZpVGZlaHFuaVJLRHBUaWtoVWMyZ0hUN1lTJTJCMEs5SEpqNnFFN3U0NUlsTjhIemVReFBFMEJaT1A4SDdtJTJGWllkJTJCSCUyQjRQR2tkTTZrUHVEMFc0Tk9UWDNMU2wxSGtCTVB5ajN0MlJNaGZ2JTJGR1BGdEtYcFdvdWcyb3B6RHk0ZzlldnpSekRFMlNnVXVMQ01RMXNKdCUyRjFueTd4MmJrRnpFbTVpTW1ZR21YMXBSa2pVVUZsSlh0ZDdCZ2glMkZGd2xrY1ZVeWtPVFNzMkUlMkJ0Mm00bWx4a1AyaGFuOTNweGJjdkkxbWdrdlolMkJpZVlJWnpzaXJRemUwaCUyRkdmdGwza0poaGhwam5URUlkY1llWUJRZzJvdXp5MVhTSHFXJTJCSXBYa1BhVmsxdmRGVyUyQlJlaXFKZTloelV0Zmgxc0VLNVlmTVRQOUtiOEVHOWQlMkZBUSUzRCUzRCUzQyUyRmRpYWdyYW0lM0UlM0MlMkZteGZpbGUlM0WY3ICmAAAgAElEQVR4Xu2dCbhVY/v/70gqGkSGXmSIiJQpZcoQoYy95qTwZngNqZ8KZSpKkcJriitDxmSqjJEhImNKKmOoDEUDTaL/9X3+7zrvbp99zlmns88561nP57mururstdZ+7s9973W++37u+1lVVq9evdoYEIAABCAAAQhAAAIQKAOBKojKMtDjVAhAAAIQgAAEIAABRwBRSSBAAAIQgAAEIAABCJSZAKKyzAi5AAQgAAEIQAACEIAAopIYgAAEIAABCEAAAhAoMwFEZZkRcgEIQAACEIAABCAAAUQlMQABCEAAAhCAAAQgUGYCiMoyI+QCEIAABCAAAQhAAAKISmIAAhCAAAQgAAEIQKDMBBCVZUbIBSAAAQhAAAIQgAAEEJV5iIEVK1bY33//bTVq1MjD1bgEBCAAAQhAAAIQ8I+AN6Ly1FNPtccee8wmTJhgBx10UCHSn376qTVr1swOOeQQe/XVVyvUE/vvv7/p/RcvXlyh78ubQQACEIAABCAAgaQQ8EZUnnzyyfbEE084wSjhmD2mTJlizZs3R1QmJbKYBwQgAAEIQAACQRFAVObB3WQq8wCRS0AAAhCAAAQg4DWB1IvK77//3vr3728TJ050jlKW8/zzz7cmTZqs4bgXXnjBnn/+efenbt26bom9bdu2dvjhh69x3Msvv2wjRoxwy93KjJ522mk2YMAAlr+9/hgweQhAAAIQgAAEykog1aLy448/ttatW9uSJUts0003tYYNG9r7779vtWrVsjFjxrjXNB566CHr1KmT+/cBBxzg/n7rrbfc388995wdffTR7t+q6VRtp8bee+9t8+bNsx9++MH9X9ekprKs4cj5EIAABCAAAQj4SsA7USlxqExi9li4cKH9/PPPBTWVq1evtn333dfeffddGz58uHXu3NmqVq1q48ePt8MOO8x22203Ux2mhrKRr7zyik2bNs122WUX97NHH33UZSG7du1qd999ty1dutQ233xzJ1Dffvttd+2//vrLunXrZrfffjui0tdPAPOGAAQgAAEIQCAvBLwTlcoI5tq6Z9myZU7wRd3fylLusccetuOOO9rMmTPXgHXooYfaa6+9ZrNmzbIddtjBnn32WVtnnXUKMpI6OBKfEpYPP/ywPfnkk3biiSc6EXnLLbcUXE/ZyTp16iAq8xKOXAQCEIAABCAAAV8JeCcq43Z/jxo1yk466SS37L3PPvus4Z/33nvPZTW1xK0mGw3VSN5///0mMfrll18WLGtHovKGG26wK6+80nWgS1xmjj333NO++OILlr99/RQwbwhAAAIQgAAEykwgtaLyrrvucg05EpXavzLXuP76622vvfZyy9yql9TYb7/9XBNPo0aNrFevXu41ZSp79OhhQ4YMccvip5xyyhqXo/u7zHHIBSAAAQhAAAIQ8JxAakWlurmPOuooO/744+2pp55aw01z58613377zS19KzPZsmVLt3ytbONmm23mjp0+fbqrr4xEpeomL7roIrv44ott2LBhBddT7aZqLbX8TqOO558Gpg8BCEAAAhCAwFoTSK2oVFf2Vltt5cD88ccfVrNmTfdviT/VWep1iUA16HTo0ME6duzousCjcc0119i1115bICrfeecdl8XcbrvtXI2mmn40xo0bZ+3bt6emcq1DkBMhAAEIQAACySXwwQcfuB1fjj32WHvmmWcqZKJ69POcOXNsgw02sHr16lXIe+bjTVIrKgVHy9eDBg1y2wQpw6is4uDBg922QldccYVp+VvZSYlMjVtvvdXq16/vhOLIkSPdz9Qlft9997llcmU+lQE98sgjrUuXLq4u88ILL3THsaVQPsKRa0AAAhCAAASSRUCaoUWLFq6ZV9sMVsSIEmPRamlFvGc+3sMbUbk2z/5evny59enTx26++eY1WGkz9J49e9p6663nfq4tg6666ionEjVUh6k6ygcffNBlL6NAWrBggZ1++un20ksvFVzv7LPPNm1npE3RWf7OR0hyDQhAAAIQgEByCCAq4/vCG1EZ36TCR86fP9+mTp1q6667ru266645U8nac1KBo0zl9ttvX3CRr776ym0ZtMkmm7ifKdupn3377bfWtGnTghrMssyPcyEAAQhAAAIQSCaB0ojKH3/80TX0Kvmkng2tlOqPEmNKWEVDO9loV5lId2gXGZXc7bzzzm7LQ62k6u9oB5s77rjDttxyy2QCyphVEKIy8V5gghCAAAQgAAEIJJJAXFG5atUqJyD10BWVxLVp08aJRi1l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mRpXIioRlekO5iz/cn9OvbtTbyCiMvUu/v+ZjsWLF7vMZCQmV65c6SzfeOONbf78+amigKhMlTsLGROaf0OzN93RmztTyf05NK+n115EZXp9W2CZnNyhQwd77rnn7M8//6wwi1u3bm16wHxljJAeS1kZfCvzPRXPoQ3iOb0er6z7c2USJZ4rk375vjeisnz5JuLqxWUq69WrZwsWLEjEPPM1CTI7+SKZzOuE5t/Q7E1m1JXfrLg/lx9brlzxBBCVFc+8wt+RmsoKR84b5pGAmsn69OljAwcOdLW/UTwPGzbMevfubf3790/V7gXZ6BCVeQymBF6K+3MCncKU1pqAt6Lyl19+sZ9//tl22WWXtTa+NCd++umntvXWW1vdunVLc1oijqX7OxFuKHYSxHPReNS8oNrfqlWrWs2aNV1mXRl27ViwatUq9/9atWol38lrOUMfRSXxHN/Z3J/js6qsI4nn+OS9FJX6RbLvvvvaTjvtZA8++KCzdvz48TZjxoyclp955pml+qXzn//8x1599VXT31tssYW75lFHHWXVqlWzZ555Jj7dhBzJPmgJcUQR08iO5+HDh9uKFSuKnLT8ecEFF7iMXVHjtddes0mTJtm0adNs8803tz322MNOPfVUJ8x8jOfLL7/chgwZYlGDmWzQ57F79+5u94I0D99EZa77s/ymmu4PPvjA5s6da9tuu60deeSR1rJly1K5btSoUTZx4kRTljpzcH8uFcZKPTgN8ZwNMJdmKA7y119/bS+99JJNnTrVmjVrZocccojtsMMOBaf4Hs/e7VN5++2320UXXWRffPGFNWrUyDniiCOOcE7KNb799ltr2LBhrA/S66+/bgcffLA7NvP6H3/8sfvF/MQTT9iJJ54Y61pJOci3D3FZuflmb3Y8165d25SdK26o4SoSiJnHqQD+yiuvLBBayuBF19p7771twoQJtsEGG5hv8Swb6tevv4bYXn/99U0ZhDRnKeVb3+P5jz/+cPfMF154oVBI9+rVy5U1xBkLFy60pk2b2g8//OC2Q8scvsVz5tx9828cXxV3jG/25tIbmfYVpRmKYjBy5Eg744wzCr0s/XL44Ye7n/sez16JSi116VvuCSecYPfff3+BY7baaivbcccd3dNhsocEZa5fwNnH6RfUrrvu6pbVs0Wl/n/MMceYAmjevHnuF7Mvw7cPcUlc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2GN5F5Wqfdxtt92Knc8hhxxSpEjOdeJff/1ld955p11xxRXu5XvuucdOOeWUWDaX5iB1wx911FGFTlFn/KRJk2y77bYrzeXK5VhlmPv27eu69X/66adyeQ8uCgEIQKA4AohK4gMCHhNQTeF9991nX3zxhVWpUmUNSzbbbDPbcMMNY1mnc5Vxa968uTt+zpw59vXXX9vee+9tqlO86qqrYl2nuIOWL19uWmLPNZRlfPfdd0vVub106VLr2LGjy05eeumlTlhusskmZZ5n9gVUv7n55pvbsmXLXL2mtixasGCBXXbZZXb//ffbmWee6f6uzPHWW2/ZgQce6KaAqKxMT/DeEAibAKIybP9jvecEJHAkdorqdlYmr1OnTm57IC2NHnrooc5iLZWee+65rv5Qmc63337bLZtGY8qUKW6pulevXm7bHnWEl9eImoMGDhzo3k9bAinjKCGnLOS6667r3vrFF190P99hhx1MGdpjjjnGxowZ48ToPvvsU6rpDRs2zBo0aGAnnnhiiedFtaZdu3Y1zTUaX331lTVq1MgJb+2XOWDAAJe1FGOxjsbgwYPdz7Wsf8YZZxT5fhLHEvI9evQocU6ZB8yfP98txTdp0sSmT5/uXiJTWSqEHAwBCOSJAKIyTyC5DAQqg0Dt2rXt2GOPdVkzLV3XrFnTdt999zX2llRDi7JpW265pRMdykhK6PTs2dO03PzKK6/YOuuss8b0R48ebf/85z/LvVFHjUDbbLONWxbXlkASkMpAygbtO3n77bfbv//9b/vtt99cE5FqJ19//XW3dZDsOOigg+zss88uhF4ZzOKGMrNt27Z1QrWk8e2337oM5b777uvmFY1oSVxCWIJ4xowZtvPOO7uXZYuOleBVrarmKhFav379It/uhBNOcFlXZUbjDh0r/4uJygtatGiBqIwLj+MgAIG8E0BU5h0pF4RAxRCQ0KpXr17ON+vTp49de+21BWLxuOOOs2effda6devmGlok0CR0ohrK7IvoKTUdOnSw7777ztVYlteI5jV+/PiCLKreS5m/KPsoUdevXz+3zK8s3k033eRE1MEHH1zktP7+++9C5QCZB5dGVGaep43hlcGVgBw+fLhjqCykMoUaQ4cOdUvx2itTc9xrr72cOH7uuedKzPaujahUU9LFF1/s5qRufZU8aJCpLK+I5boQgEBxBBCVxAcEPCWgJW+JFg1lyrS1jjJvDzzwgFvuvvXWW+2iiy5yr8+bN891guvnairRMutDDz3kahLzNdQdrdo+LRPHGeqilvjS02+05J09VMcpMRnNV8u7H3zwgdWoUSPO5Ys9Zm1FZabY1Rto6Vud8tFTh1RuILErDtG8lUmN041dWlEZ+V8d6A8//LCzF1FZ5tDgAhCAQBkIICrLAI9TIVCZBCQUtZ2QsmSZy7LRkmt2w8aoUaPspJNOclNWLeETTzyR1+lr6faaa64x1WPGGaovVId6UTWRqvGU6IzqBKMl5TjXzj5Gy+gS0tFQp7v4ZHbHaylddZrFDdWiKnMqQacSATGVeNTSdjSiWkv9XyUHygarTCF7aPlcpQfR0LV++OEHl+mMhrZYylVjqX045fPff//dZU032mgjROXaBAbnQAACeSWAqMwrTi4GgWQQUMZK9YcLFy50T57R0PK3lps1JOhUa5nPURpR+c033zgxpmd2F9UR/ueff1rLli1dfaLGtGnTCpaZSztvNTSpGam4obrUQYMGFTpEzUx//PGHE6FVq1YteF2CTs0+yv5K+Eb1lFGdqA6Ujap1VK1r9tA2Ttddd12xc1KtaS6RLjEuH0q0KlsaDflAQ01BOlcinwEBCECgogggKiuKNO8DgTwT0JLx999/7zbgjoSj3kJCMspcKbOm5pdffvnFPSVHAkh1gPpbAiQSmWs7NdUuNm3a1J2uLmQJWS1TayjDdtZZZ+W8tMSURJVqEDM7pTMPztx3UddV1lJZzbV5/KK2AMrsblcG8IADDnD7cUZDXHJtZK4SAmU6n3nmGdcUkzmOOOIIe+mll9yG8Vr2Fg9tOq//S4Rq3so8Zj5KMjpfojTzyT9ipWtpO6doVKtWLec2SfKdaimzhzKdGhKbEtKPPvro2rqW8yAAAQiUmgCistTIOAECySAg0Saxom1uMusYo27vzI3Eteyt5VXVKWo/wzZt2jgB9eWXXzrxU5ahzmiNiRMnuuVsPTNcQzWc2nIn11BHtARiUY+BjOotNUct72pDc9UpSoxqg++yjtLUVGpbowsuuMB1mWfWRkrARU1MauBRdviOO+5w3erahkm8ozrWCRMmuE714kZpaypzXUtfHCRWadQpa4RwPgQgsDYEEJVrQ41zIJAAAmpaiZY+tfG3MnlqlolEl5Z7tQ1O9HQcLcVqCVmNLueff74Tf/msrYy7/B1lUpVNU6Y1e2iTdG0ZpCXlESNGWOfOnZ341f6UGmWprYzeqzSiUvNVI46yu5qLxLpEr5pjosdDSnhmzlF+UId9xL642spoTojKBHyomAIEIFAmAojKMuHjZAhULgHVSSpLKXETDWUe1QGupVktSUtMShBpi5vWrVu7wySUlEXTeepe1vZBZR1aHtaSdkmNOupQP/LII4us64yWxiXetNVQ9KQgNdd0797dLa+rTjF7b83SzF/X1Byef/75WKep61tb9mQ2++hELW2rQ13PAlcGWNlU/V9bOkUj2qRdy+jqyC9qICpjuYKDIACBBBNAVCbYOUwNAnEIrFy50i0RS0BqI/GGDRsWPIUmzvkcE4+AGockKrVkX7duXbe0X9Q+ofGuyFEQgAAE0kUAUZkuf2INBCAAAQhAAAIQqBQCiMpKwc6bQgACEIAABCAAgXQRQFSmy59YAwEIQAACEIAABCqFAKKyUrDzphCAAAQgAAEIQCBdBBCV6fIn1kAAAhCAAAQgAIFKIYCorBTsvCkEIAABCEAAAhBIF4H/B3+vRIg9ZP1TAAAAAElFTkSuQmCC)\n",
        "\n",
        "\n",
        "\n",
        "\n"
      ],
      "metadata": {
        "id": "gjtY9l5XE9tX"
      }
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "C29C-MwcL0Iy",
        "outputId": "47b90925-d44a-4c14-a506-3d29b466171a"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Overwriting parcial.h\n"
          ]
        }
      ],
      "source": [
        "%%writefile parcial.h\n",
        "\n",
        "#ifndef POLINOMY_H_\n",
        "#define POLINOMY_H_\n",
        "\n",
        "#include<iostream>\n",
        "#include <string>\n",
        "#include<bits/stdc++.h>\n",
        "#include <ctime> \n",
        "#include <random>\n",
        "\n",
        "using namespace std;\n",
        "\n",
        "class NodeTerm{\n",
        "  public:\n",
        "    long int m_Coeff;\n",
        "    int m_Exp;\n",
        "    NodeTerm *m_pNext;\n",
        "    NodeTerm *m_pPrev;\n",
        "  public:\n",
        "    NodeTerm(long int c, int e){\n",
        "      m_Coeff = c;\n",
        "      m_Exp = e;\n",
        "      m_pNext = 0;\n",
        "      m_pPrev = 0;\n",
        "    }\n",
        "\n",
        "    long int calculate(int x){\n",
        "      return m_Coeff*pow(x,m_Exp);\n",
        "    }\n",
        "};\n",
        "\n",
        "class Polinomy{\n",
        "public:\n",
        "    NodeTerm * m_pHead;\n",
        "\t  NodeTerm * m_pLast;\n",
        "public:\n",
        "    Polinomy(){\n",
        "      m_pHead = m_pLast = 0;\n",
        "\n",
        "    }\n",
        "\n",
        "    void addTermAtLast(long int coeff, int exp)\n",
        "    {\n",
        "      //Implementar una funcion que me permita insertar al final del polinomio\n",
        "    }\n",
        "\n",
        "    void addTerm(long int coeff, int exp){\n",
        "      // Implementar una funcion que inserte un nuevo termino en el polinomio de manera ordenanda (el mayor grado va a la izquierda o en la cabeza).\n",
        "      // Si se tienen dos terminos con el mismo grado, estos se combinan por medio de la adición.\n",
        "    }\n",
        "\n",
        "    long int calculate(int x){\n",
        "      // Implementar método que calcula el valor final del polinomio si reemplazamos la variable independiente X.\n",
        "    }\n",
        "\n",
        "    Polinomy operate(Polinomy p2){\n",
        "      // Implementar un método que opera sobre dos polinomios y me genera uno nuevo.\n",
        "    }\n",
        "\n",
        "  \n",
        "    void print()\n",
        "    {\n",
        "      NodeTerm * tmp = m_pHead;\n",
        "      while(tmp!=0)\n",
        "      {\n",
        "        cout<<tmp->m_Coeff<<\"X^\"<<tmp->m_Exp<<\" \";\n",
        "        tmp = tmp->m_pNext;\n",
        "      }\n",
        "      cout<<endl;\n",
        "    }\n",
        "};\n",
        "\n",
        "#endif /* POLINOMY_H_ */"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "-ItaBY4yMCMR",
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "f9e62aab-2749-42b0-f8c2-41d0f9406b23"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Overwriting main.cpp\n"
          ]
        }
      ],
      "source": [
        "%%writefile main.cpp\n",
        "#include \"parcial.h\"\n",
        "\n",
        "int MINNUMBER = 1;\n",
        "int MAXNUMBER = 10;\n",
        "int NUMBER_INSERTIONS = 100;\n",
        "\n",
        "\n",
        "//Prueba 1: Se evalua si después de varias inserciones el polinomio calcula el valor correcto. (6 puntos)\n",
        "void Test1(Polinomy p){\n",
        "  mt19937 mt_coeff(2012);\n",
        "  mt19937 mt_exp(2016);\n",
        "  for(int i=0; i < NUMBER_INSERTIONS; i++){\n",
        "    p.addTerm(MINNUMBER + (mt_coeff()%MAXNUMBER), MINNUMBER +(mt_exp()%MAXNUMBER));\n",
        "  }\n",
        "\n",
        "  long int result = 0;\n",
        "  mt19937 mt_x(2000);\n",
        "  for(int i=0; i<3; i++){\n",
        "    int x = MINNUMBER + (mt_x()%MAXNUMBER);\n",
        "    cout<<\"X = \"<<x<<endl;\n",
        "    result = p.calculate(x);\n",
        "    cout<<\"Operation \"<<i<<\":\"<<result<<endl;\n",
        "  }\n",
        "}\n",
        "\n",
        "// Prueba 2: Se comprueba si al hacer varias inserciones sobre 2 polinomios y el reemplezar la variable independiente sobre el resultado de combinar\n",
        "// estos dos polinomios, el resultado es el correcto. (6 Puntos)\n",
        "void Test2(Polinomy p1, Polinomy p2){ \n",
        "  mt19937 mt_coeff(2012);\n",
        "  mt19937 mt_exp(2016);\n",
        "  for(int i=0; i < NUMBER_INSERTIONS; i++){\n",
        "    p1.addTerm( MINNUMBER + (mt_coeff()%MAXNUMBER), MINNUMBER + (mt_exp()%MAXNUMBER));\n",
        "    p2.addTerm( MINNUMBER + (mt_coeff()%MAXNUMBER), MINNUMBER + (mt_exp()%MAXNUMBER));\n",
        "  }\n",
        "\n",
        "  Polinomy p3 = p1.operate(p2);\n",
        "\n",
        "  p3.print();\n",
        "  long  result = 0;\n",
        "  mt19937 mt_x(2000);\n",
        "  for(int i=0; i<3; i++){\n",
        "    int x = MINNUMBER + (mt_x()%MAXNUMBER);\n",
        "    cout<<\"X = \"<<x<<endl;\n",
        "    result = p3.calculate(x);\n",
        "    cout<<\"Operation \"<<i<<\":\"<<result<<endl;\n",
        "  }\n",
        "}\n",
        "\n",
        "int main()\n",
        "{\n",
        "    Polinomy p1, p2, p3;\n",
        "    cout<<\"Test 1\"<<endl;\n",
        "    Test1(p1);\n",
        "    cout<<\"Test 2\"<<endl;\n",
        "    Test2(p2,p3);\n",
        "\n",
        "    return 1;\n",
        "}"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "07a0J8zFMMmE"
      },
      "outputs": [],
      "source": [
        "\n",
        "!g++ parcial.h main.cpp  -o main.o\n",
        "!./main.o\n",
        "\n"
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "PARTE 2: Pilas y Vectores\n",
        "\n",
        "Dado que tenemos una estructura de pilas, se quiere implementar una clase que me consiga siempre retornar el Máximo o el Mínimo Punto dentro de la pila en referencia a un punto fijo. Es decir, mi clase siempre tendrá un punto X, donde cada nuevo elemento que iré insertando tendra que ser comparado mediante una distancia **Euclidiana**, de esta manera, puedo saber si los nuevos puntos están mas cerca o mas lejanos de mi punto de referencia X. \n",
        "\n",
        "**Nota**: Considerar los ejercicios implementados en clase.\n",
        "\n",
        "Considerar lo siguiente:\n",
        "\n",
        "1. La clase no será solo de mínimos o máximos, ahora se pide que se tenga un puntero a una función (pref, p1, p2) donde la función puede variar, es decir, que puede tener una función que puede determinar si p1 es mas cercanos a pf que p2. Dando una flexibilidad de tener una misma clase para determinar puntos cercanos o lejanos.\n",
        "\n",
        "2. El ejercicio pide implementar dor nuevas funciones para poder tener dos instancias de la clase **PointStack**. Uno para los mas cercanos y otro para los mas lejanos.\n",
        "\n"
      ],
      "metadata": {
        "id": "ShTUKCsRXP1D"
      }
    },
    {
      "cell_type": "code",
      "source": [
        "%%writefile parcial_part2.h\n",
        "\n",
        "#ifndef MAXSTACK_H_\n",
        "#define MAXSTACK_H_\n",
        "\n",
        "#include<iostream>\n",
        "#include <string>\n",
        "#include<bits/stdc++.h>\n",
        "#include <ctime> \n",
        "#include <tuple>\n",
        "#include <random>\n",
        "\n",
        "\n",
        "using namespace std;\n",
        "\n",
        "class EmptyStack : public runtime_error {\n",
        "public:\n",
        "  EmptyStack(const string& msg = \"\") : runtime_error(msg) {}\n",
        "};\n",
        "\n",
        "template <class T>\n",
        "class Node{\n",
        "  public:\n",
        "    T m_Data;\n",
        "    Node<T> *m_pNext;\n",
        "  public:\n",
        "    Node(T d){\n",
        "      m_Data = d;\n",
        "      m_pNext = 0;\n",
        "    }\n",
        "};\n",
        "\n",
        "template <class T>\n",
        "class Stack{\n",
        "public:\n",
        "    Node<T> * m_pTop;\n",
        "public:\n",
        "    Stack(){\n",
        "      m_pTop = 0;\n",
        "    }\n",
        "\n",
        "    void push(T d)\n",
        "    {\n",
        "      Node<T> *pNew = new Node<T>(d);\n",
        "      if (!m_pTop){\n",
        "        m_pTop = pNew;\n",
        "      } else {\n",
        "        pNew->m_pNext = m_pTop;\n",
        "        m_pTop = pNew;\n",
        "      }\n",
        "    }\n",
        "\n",
        "    T pop(){\n",
        "      if (!m_pTop){\n",
        "        throw EmptyStack(\"No hay elementos\");\n",
        "      }\n",
        "      Node<T> *tmp = m_pTop;\n",
        "      m_pTop = tmp->m_pNext;\n",
        "      T data = tmp->m_Data;\n",
        "      delete(tmp);\n",
        "      return data;\n",
        "    }\n",
        "\n",
        "    T top(){\n",
        "      if (!m_pTop){\n",
        "        throw EmptyStack(\"No hay elementos\");\n",
        "      }\n",
        "      return m_pTop->m_Data;\n",
        "    }\n",
        "\n",
        "    bool isEmpty(){\n",
        "      return m_pTop == 0;\n",
        "    }\n",
        "\n",
        "    void print()\n",
        "    {\n",
        "      Node<T> * tmp = m_pTop;\n",
        "      while(tmp!=0)\n",
        "      {\n",
        "        cout<<tmp->m_Data<<\" \";\n",
        "        tmp = tmp->m_pNext;\n",
        "      }\n",
        "      cout<<endl;\n",
        "    }\n",
        "};\n",
        "\n",
        "class Point{\n",
        "public:\n",
        "  float m_X;\n",
        "  float m_Y; \n",
        "  float m_Z;\n",
        "public:\n",
        "  Point(){\n",
        "    m_X = m_Y = m_Z = 0.0;\n",
        "  }\n",
        "  Point(float x, float y, float z){\n",
        "    m_X = x;\n",
        "    m_Y = y;\n",
        "    m_Z = z;\n",
        "  }\n",
        "\n",
        "  float distance(Point p2){\n",
        "    // Implementar la funcion distancia euclidiana\n",
        "  }\n",
        "\n",
        "  friend ostream& operator<<(ostream& os, const Point& p)\n",
        "  {\n",
        "      os << \"(\"<<p.m_X<<\", \"<<p.m_Y<<\", \"<<p.m_Z<<\")\";\n",
        "      return os;\n",
        "  }\n",
        "\n",
        "};\n",
        "\n",
        "\n",
        "class PointStack{\n",
        "public:\n",
        "  Point m_Point;\n",
        "  bool (*m_compFunc) (Point, Point, Point);\n",
        "  Stack<Point> m_S;\n",
        "  Stack<Point> m_auxS;\n",
        "public:\n",
        "  PointStack(){\n",
        "    m_compFunc = 0;\n",
        "  }\n",
        "  PointStack(Point p, bool (*compFunc) (Point, Point, Point)){\n",
        "    m_Point = p;\n",
        "    m_compFunc = compFunc;\n",
        "  }\n",
        "\n",
        "  void push(float x, float y, float z){\n",
        "   // Implmentar un push a nuestras pilas\n",
        "  }\n",
        "\n",
        "  bool isEmpty(){\n",
        "    return m_S.isEmpty();\n",
        "  }\n",
        "\n",
        "  tuple<Point, Point>  pop(){\n",
        "    // Pueden cambiar a voluntad esta funcion \n",
        "    // en el caso de no cambiarlo, una tupla puede ser evaluada usando get<index>(variable tuple), por ejemplo:\n",
        "    // tuple<point, point> mytuple= make_tuple(p1, p2), donde,\n",
        "    // get<0>(mytuple) me irá a retornar el valor de p1\n",
        "    return make_tuple(m_S.pop(), m_auxS.pop());\n",
        "  }\n",
        "\n",
        "  float meanDistanceFromN(int n){\n",
        "    // Implementar una funcion que me determina la diferencia en la distancia promedio de los n ultimos elementos\n",
        "    // (hacer push de n elementos) y el top de la pila auxiliar después de haber sacado estos n elementos.\n",
        "    // La diferencia es un valor absoluto.\n",
        "  }\n",
        "\n",
        "  void print(){\n",
        "    cout<<\"S:\"<<endl;\n",
        "    m_S.print();\n",
        "    cout<<\"Aux S\"<<endl;\n",
        "    m_auxS.print();\n",
        "  }\n",
        "};\n",
        "\n",
        "// Implementar 2 funciones extras para determinar si son cercanos o lejanos los puntos en relación a un punto de referencia.\n",
        "//bool func1(Point pref, Point p1, Point p2)\n",
        "//bool func2(Point pref, Point p1, Point p2)\n",
        "\n",
        "#endif /* MAXSTACK_H_ */"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "SWzi6TIneZtE",
        "outputId": "6afaa71c-c229-4e24-eed7-ed3dd4eaa804"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Overwriting parcial_part2.h\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "%%writefile main.cpp\n",
        "#include \"parcial_part2.h\"\n",
        "\n",
        "int MINNUMBER = 1;\n",
        "int MAXNUMBER = 10;\n",
        "\n",
        "int NUMBER_POP = 8;\n",
        "int NUMBER_INSERTIONS = NUMBER_POP*10;\n",
        "\n",
        "\n",
        "// Prueba 3: Evalua si se implementó dos instancias  para almacenar los puntos mas cercanos y mas distances.\n",
        "// 8 Puntos  (4 si es correcto para puntos cercanos y 4.5 para mas distantes)\n",
        "\n",
        "void test(PointStack points, bool (*func)(Point, Point, Point)){\n",
        "  mt19937 mt_x(2012);\n",
        "  mt19937 mt_y(2016);\n",
        "  mt19937 mt_z(2018);\n",
        "\n",
        "  float x = MINNUMBER + (mt_x()%MAXNUMBER);\n",
        "  float y = MINNUMBER + (mt_y()%MAXNUMBER);\n",
        "  float z = MINNUMBER + (mt_z()%MAXNUMBER);\n",
        "\n",
        "  Point mainPoint(x,y,z);\n",
        "  points = PointStack(mainPoint, func);\n",
        "\n",
        "\n",
        "  for(int i=0; i<NUMBER_INSERTIONS; i++)\n",
        "  {\n",
        "    float x = MINNUMBER + (mt_x()%MAXNUMBER);\n",
        "    float y = MINNUMBER + (mt_y()%MAXNUMBER);\n",
        "    float z = MINNUMBER + (mt_z()%MAXNUMBER);\n",
        "\n",
        "    points.push(x,y,z);\n",
        "  }\n",
        "  \n",
        "  for(int i = 0; i < 3; i++){\n",
        "    cout<<\"Test \"<<i<<\":\"<<endl;\n",
        "    cout<<points.meanDistanceFromN(NUMBER_POP)<<endl;\n",
        "  }\n",
        "}\n",
        "\n",
        "int main()\n",
        "{\n",
        "    cout<<\"_____Min Points___\"<<endl;\n",
        "    PointStack pmin;\n",
        "    test(pmin, TU_FUNCION);\n",
        "\n",
        "    cout<<\"_____Max Points____\"<<endl;\n",
        "    PointStack pmax;\n",
        "    test(pmax, TU_FUNCION);\n",
        "    \n",
        "    return 1;\n",
        "}"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "t4Gy6Gjkgi7M",
        "outputId": "bb1d2610-ed13-4a68-a7ae-dd76f12d6e86"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Overwriting main.cpp\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "\n",
        "!g++ parcial_part2.h main.cpp  -o main.o\n",
        "!./main.o\n",
        "\n"
      ],
      "metadata": {
        "id": "3X2qZt4-gqCu"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [],
      "metadata": {
        "id": "bf0QxRCPgqeQ"
      },
      "execution_count": null,
      "outputs": []
    }
  ],
  "metadata": {
    "colab": {
      "collapsed_sections": [],
      "provenance": [],
      "include_colab_link": true
    },
    "kernelspec": {
      "display_name": "Python 3",
      "name": "python3"
    },
    "language_info": {
      "name": "python"
    }
  },
  "nbformat": 4,
  "nbformat_minor": 0
}
