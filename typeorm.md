## How To use the whereIn condition in findAndCount TypeORM repository

To use the whereIn condition in findAndCount TypeORM repository, you can pass an array of values to the whereIn parameter, which will filter the results based on whether a specified column's value matches any of the values in the array.

Here's an example:

```
import { EntityRepository, Repository } from 'typeorm';
import { User } from '../entities/user.entity';

@EntityRepository(User)
export class UserRepository extends Repository<User> {
  async findAndCountUsersWithIds(ids: number[]): Promise<[User[], number]> {
    const [users, count] = await this.findAndCount({
      where: {
        id: In(ids),
      },
    });
    return [users, count];
  }
}
```

In this example, we have a User entity and a UserRepository repository. We want to find and count all users with IDs that match any of the IDs in the ids array. We pass an object to the where parameter with the condition { id: In(ids) }.

Note that we use the In function to create the whereIn condition. The In function is imported from the typeorm package, and it takes an array of values as its argument.

You can also use the NotIn function to create the opposite condition, where the specified column's value does not match any of the values in the array.

For more information on how to use the findAndCount method and its parameters, you can refer to the official [TypeORM documentation](https://typeorm.io/#/find-options/find-and-count-options)