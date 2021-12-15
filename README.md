**Nome:** Vitor Franco Rezende

**Matrícula:** 2017014723

**Projeto:** LegoFy (https://github.com/JuanPotato/Legofy)

Legofy é um programa python que pega uma imagem estática ou gif e faz com que pareça ter sido construído com LEGO.

**Teste 1**
```python
    def test_legofy_image(self):
        self.create_tmpfile('.png')
        self.assertTrue(os.path.exists(FLOWER_PATH),
                        "Could not find image : {0}".format(FLOWER_PATH))

        legofy.main(FLOWER_PATH, output_path=self.out_path)
        self.assertTrue(os.path.getsize(self.out_path) > 0)

    def test_legofy_gif(self):
        self.create_tmpfile('.gif')
        gif_path = os.path.join(TEST_DIR, '..', 'legofy', 'assets', 'bacon.gif')
        self.assertTrue(os.path.exists(gif_path),
                        "Could not find image : {0}".format(gif_path))
        legofy.main(gif_path, output_path=self.out_path)
        self.assertTrue(os.path.getsize(self.out_path) > 0)
```
Inicialmente temos esses dois Testes de Unidade, eles basicamente verificam a criação dos arquivos temporários referentes a imagem e gif respectivamente, que foram criados e aferem se é o possível ou não realizar o Legofy. Dessa forma nos dois casos, os testes realizam a criação do arquivo com o formado desejado para teste, verificam se a criação obteve êxito e então testam se é possível aplicação da ferramenta.


**Teste 2**
```python
    def test_get_new_filename(self):
        new_path = legofy.get_new_filename(FLOWER_PATH)
        self.assertTrue(os.path.dirname(FLOWER_PATH) ==
                        os.path.dirname(new_path))

        self.assertFalse(os.path.exists(new_path),
                         "Should not find image : {0}".format(new_path))

        self.assertTrue(new_path.endswith('_lego.jpg'))
        new_path = legofy.get_new_filename(FLOWER_PATH, '.gif')
        self.assertTrue(new_path.endswith('_lego.gif'))

```
Nesse Teste de Unidade temos a verificação da geração de nome do arquivo de saída, se o caminho gerado é único e também testa as extensões do arquivo de saída após aplicação na ferramenta, Legofy.

**Teste 3**
```python
    def test_bad_image_path(self):
        fake_path = os.path.join(TEST_DIR, 'fake_image.jpg')
        self.assertFalse(os.path.exists(fake_path),
                         "Should not find image : {0}".format(fake_path))
        self.assertRaises(SystemExit, legofy.main, fake_path)

```
O Teste 3 é bastante simples, ele apenas realiza a verificação de que, se uma imagem for passada em um diretório invalido, a ferramenta não da sequência no procedimento de Legofy. Dessa forma ele primeiro cria uma imagem em um diretório fake e verifica se o diretório é válido, caso não seja, da exit no procedimento.
