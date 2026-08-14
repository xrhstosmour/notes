#ruby #rails #facades #design-patterns #architecture

A facade wraps a complex subsystem, a set of models, an external service, several other objects, behind a single, simplified interface. Unlike a [[Service Objects|service object]], a facade doesn't necessarily perform an action, it can just be a read-oriented adapter that hides how the underlying data is actually assembled.

``` ruby
class ListingPageFacade
  def initialize(category, current_user)
    @category = category
    @current_user = current_user
  end

  def filters
    @category.filters.applicable_to(@current_user)
  end

  def featured_items
    @category.items.featured.limit(10)
  end
end

# In a serializer or controller, instead of reaching into several models directly:
ListingPageFacade.new(category, current_user).featured_items
```

Reach for a facade when some logic doesn't belong to a specific view (ruling out a [[Presenters|presenter]]) and isn't a standalone class method or constant (ruling out a plain helper or [[Concerns|concern]]), typically controller-adjacent logic that several serializers or views need to share.
