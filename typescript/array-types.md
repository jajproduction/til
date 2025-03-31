# Array Types

In TypeScript, you add `[]` after the type to indicate it's an array.

```ts
interface OrdersProps {
  sales_id: number;
  total_amount: number;
  total_discount: number;
  sale_date: string;
  customer: {
    name: string;
  };
  saleitems: {
    sale_item_id: number;
    quantity: number;
    price: number;
    discount_value: number;
    subTotal: number;
    product: {
      name: string;
    };
  }[];
}
```
