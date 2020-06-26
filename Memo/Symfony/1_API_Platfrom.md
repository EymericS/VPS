# API Platfrom

Official website [here](https://api-platform.com/).
MOC youtube [video](https://www.youtube.com/watch?v=Neb4GBRP7eg) from [Grafikart](https://www.grafikart.fr/)

## Symfony install

* `~/project$ composer require api`
* now accesible from `domain.tld/api`

## Config in Symfony

* in : `~/project/config/api_platform.yaml`
* linked **to nelmio_cors** : `~/project/config/nelmio_cors.yaml`

## Entity.php Annotation

### Make it API Platform readable

* Entity *(Comment.php)* :
	* + `use ApiPlatform\Core\Annotation\Resource;`
	* + `@ApiRessource()`
* param :
	* control **collection operation** `collectionOperations={"GET", "POST", "PUT", "PATCH", "DELETE"},`
	* control **item operation** : `itemOperation={"GET", "POST", "PUT", "PATCH", "DELETE"}`,
	* control **context** : `normalizationContext={"groups"={"read:comment"}},
	* control **pagination** : `paginationItemsPerPage=2,`
	* attribute :
```
attributes={
	"order"={"publishedAt":"DESC"}				// publishedAt an attr of our Entity
}
```

### Make it API Platform usable

* Entity:attr + `@Groups({"read:comment"})

### Filter system

Documentation for [filter](https://api-platform.com/docs/core/filters/)
* Entity :
	* + `use ApiPlatform\Core\Annotation\ApiFilter;`
	* + `@ApiFilter()`
* param : :
	* + `use ApiPlatform\Core\Bridge\Doctrine\Orm\Filter\SearchFilter;`
	* filter type : `SearchFilter::class`
	* props for : `properties={"post": "exact"}

### Relation

Return relatedEntity:attr : 
* + `@Groups({"read:comment"})

## API Platform Controller
Oficial doc for [controller](https://api-platform.com/docs/core/controllers/#creating-custom-operations-and-controllers)
Add to `@ApiResource(...)`:
```
collectionOperation={
	...
	"post"={
		"security"="is_granted('IS_AUTHENTICATED_FULLY')",
		"controller"=App\Controller\Api\CommentCreateController::class
```

# TODO
[x] install
[ ] normalization ?
[ ] denormalization ?
