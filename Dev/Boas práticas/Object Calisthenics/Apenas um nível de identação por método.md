Uma das regras que aplicam muito forte o [[Single Responsibility Principle]] pois um método com muitos níveis de identação pode muito bem significar que ele está realizando muito mais ações do que ele deveria.

Um método de refatoração muito usado para aplicar essa regra em códigos já existentes é o método de [[Extração]], pois cada nível de identação após o primeiro pode ser extraido para uma nova função que realize apenas aquela ação.

``` php
<?php

public function show($slug)
{

	$lesson = $this->repository->findBySlug($slug);
	
	if ($lesson) {
		
		if (!empty($lesson->thumb_url)) {	
			$this->seo()->addImages($lesson->thumb_url);
		}
		
		if ($lesson->track) {	
			$this->seo()->setTitle($lesson->title.' ['.$lesson->track->title.']');
		} else {
			$this->seo()->setTitle($lesson->title);
		}
		
		$this->seo()->setDescription($lesson->description);
		
		return $this->view('lessons::show')->with(compact('lesson'));
	}

	return redirect(route('lesson.index'));
}
```

Nesse caso com uma aplicação do método de extração e um ternário já é possível remover um nível da identação, aplicar a legibilidade do código e ainda seguir o SRO.