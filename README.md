import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Badge } from "@/components/ui/badge";
import { Button } from "@/components/ui/button";

const recipes = [
  {
    name: "American Pancakes",
    category: "Breakfast",
    image: "https://source.unsplash.com/featured/?pancakes",
    instructions:
      "Dry ingredients (Bowl 1): 2 Cups of flour, 3 tbsp sugar, 1 tbsp baking powder, pinch of salt. Wet ingredients (Bowl 2): 2 eggs, 1.5 cups of milk, 1 tsp vanilla extract, 3 tbsp melted butter. Mix bowl 1 and 2, cook on medium heat.",
    link: null,
  },
  {
    name: "Baklave",
    category: "Dessert",
    image: "https://source.unsplash.com/featured/?baklava",
    instructions: "Check the video recipe.",
    link: "https://youtu.be/e-O_1cGanGE?si=ETyamFEbycEkuTWv",
  },
  {
    name: "Bakpao",
    category: "Snack",
    image: "https://source.unsplash.com/featured/?bao",
    instructions:
      "600 g flour, 300 g lukewarm water, 2.5 tbsp dry yeast, 1 tbsp sugar, 2 tbsp oil. Knead into a soft dough. Let rise 1 hour. Fill and steam 15 minutes.",
    link: null,
  },
  {
    name: "Big Mac Sauce",
    category: "Sauce",
    image: "https://source.unsplash.com/featured/?sauce",
    instructions:
      "Ketchup, mayonnaise, mustard, vinegar, chopped pickles, onion powder, garlic powder. Mix and chill.",
    link: null,
  },
  {
    name: "Burek",
    category: "Main Dish",
    image: "https://source.unsplash.com/featured/?burek",
    instructions:
      "500 g filo sheets, 750 g minced meat, 1 onion, salt, pepper. Layer with meat mixture, roll and bake. See video for full method.",
    link: "https://youtu.be/SDdgYUQAF2A?feature=shared",
  },
  {
    name: "Chai Sugar Cookies",
    category: "Dessert",
    image: "https://source.unsplash.com/featured/?cookies",
    instructions:
      "1/2 cup unsalted butter, 1/2 cup sugar, 1 egg, 1 tsp vanilla, 1.5 cups flour, 1 tsp baking powder, chai spices. Bake at 180°C for 10-12 mins.",
    link: "https://www.youtube.com/watch?v=69cbYf79gKc",
  },
];

const categories = ["All", ...new Set(recipes.map((r) => r.category))];

export default function RecipeApp() {
  const [search, setSearch] = useState("");
  const [selectedCategory, setSelectedCategory] = useState("All");

  const filtered = recipes
    .filter((r) => {
      const matchesSearch = r.name.toLowerCase().includes(search.toLowerCase());
      const matchesCategory =
        selectedCategory === "All" || r.category === selectedCategory;
      return matchesSearch && matchesCategory;
    })
    .sort((a, b) => a.name.localeCompare(b.name));

  return (
    <div className="p-6 max-w-5xl mx-auto">
      <h1 className="text-3xl font-bold mb-4">Recipe Book 📖</h1>
      <Input
        placeholder="Search recipes..."
        value={search}
        onChange={(e) => setSearch(e.target.value)}
        className="mb-4"
      />
      <div className="flex flex-wrap gap-2 mb-6">
        {categories.map((cat) => (
          <Button
            key={cat}
            variant={selectedCategory === cat ? "default" : "outline"}
            onClick={() => setSelectedCategory(cat)}
          >
            {cat}
          </Button>
        ))}
      </div>
      <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
        {filtered.map((recipe, i) => (
          <Card key={i} className="hover:shadow-xl transition overflow-hidden">
            <img
              src={recipe.image}
              alt={recipe.name}
              className="w-full h-40 object-cover"
            />
            <CardContent className="p-4">
              <h2 className="text-xl font-semibold mb-2">{recipe.name}</h2>
              <Badge className="mb-2">{recipe.category}</Badge>
              <p className="text-sm whitespace-pre-wrap mb-2">
                {recipe.instructions}
              </p>
              {recipe.link && (
                <a
                  href={recipe.link}
                  target="_blank"
                  rel="noopener noreferrer"
                  className="text-blue-600 underline text-sm"
                >
                  Watch Video
                </a>
              )}
            </CardContent>
          </Card>
        ))}
      </div>
    </div>
  );
}
