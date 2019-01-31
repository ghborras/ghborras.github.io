---
layout: post
title: Upload images in Symfony 4.2 
---

*{{ page.date | date: "%B %e, %Y" }}*


Entity Product

~~~
 class Product
{
    ........

     /**
     * @var string
     *
     * @ORM\Column(name="foto", type="string", length=255)
     */
    private $foto;

    ........
}
~~~

ProductType

~~~
class ProductType extends AbstractType
{
    public function buildForm(FormBuilderInterface $builder, array $options)
    {
        $builder
        
        ........

        ->add('foto', FileType::class,  array(
            'attr' => array('onchange'=>'onChange(event)', 'id'=>'image',  'class'=>'mt-4') ))

        .......
        ;
    }
}
~~~

ProductController


~~~

    /**
     * @Route("/productnew", name="newproduct")
     */
    public function new(Request $request)
    {
        $product = new Product();
        $form = $this->createForm(ProductType::class, $product);
        $form->handleRequest($request);
        if ($form->isSubmitted() && $form->isValid()) {
            $product = $form->getData();
            $file = $form["foto"]->getData();
            $ext = $file->guessExtension();
            $fileName = time().'.'.$ext;
            $file->move("productImg", $fileName);
            $product->setFoto($fileName);
            $entityManager = $this->getDoctrine()->getManager();
            $entityManager->persist($product);
            $entityManager->flush();
            $this->addFlash(
                'notice',
                'Your product were saved!'
            );
            return $this->redirectToRoute('product');
        }
        return $this->render('product/productform.html.twig', array(
            'form' => $form->createView(),
        ));
    }

~~~


[close]({{ site.baseurl }}/)

